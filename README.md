# Economat

## Information Architecture

#### Resource

A naturally-occuring resource.

- Properties
  - Quantity: positive number or infinite
  - Replenishment rate: positive number, or 0
  - Position: latitude, longitude, elevation, or ubiquitous

#### Product

A physical good created by refining resources and/or other products.

- Properties
  - Unit volume: positive number
  - Unit mass: positive number
  - Tags: List of strings

#### Stock

A collection of 0 or more units of one Product.

- Properties
  - Quantity: positive number, or 0
- Links
  - Product [Cardinality: 1]

#### Stockpile

A collection of Stocks, with upper bounds on the volume, and optionally the mass, of the Products therein.

- Properties
  - Volume limit: positive number
  - Mass limit: positive number, or infinite
- Links
  - Stock [Cardinality: >= 0]

#### Process

A recipe for producing one or more Products from Resources and/or other Products.

- Properties
  - Input quantities: positive numbers, amount of each Resource/input Product required for 1 production cycle.
  - Output quantities: positive numbers, amount of each output Product produced by 1 production cycle.
- Links
  - Resource [Cardinality >= 0]
  - Product (input) [Cardinality >= 0]
  - Product (output) [Cardinality >= 1]

#### Producer

A productive node that implements one or more Processes.

- Properties
  - Throughput per process: The number of cycles for each process that can occur in parallel at the same time.
  - Position: latitude, longitude, elevation
- Links
  - Process [Cardinality >= 1]
  - Stockpile (input) [Cardinality >= 1]
  - Stockpile (output) [Cardinality >= 1]

#### Consumer

A non-productive user of Products.

- Properties
  - Position: latitude, longitude, elevation
- Links
  - Stockpile [Cardinality >= 1]

#### Transporter

A mobile Stockpile of Products and/or Resources

- Properties
  - Maximum velocity: positive number
- Links
  - Stockpile [Cardinality: 1]

#### Road

Infrastructure that interconnects all nodes with a Position.

- Properties
  - Transporter capacity: Number of Transporters able to occupy the Road at one time
  - Position: latitude, longitude, elevation
- Links
  - Transporter [Cardinality >= 0]
