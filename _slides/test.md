


[# slide 2](
layout: false
.left-column[
]
.right-column[
  # What is this about
]





layout: false
.left-column[
  Summary
  ## N-Tiers
]
.right-column[
  
  ## Benefits
    - SOLID principles
  
  ## Drawbacks
    - Not enough

]



layout: false
.left-column[
  Summary
  ## N-Tiers
  ## C.Q.R.S.
]
.right-column[
  ## Command & Query Responsibility Segregation
  - What is a Command ?
  - What is a Query ?
  - Why separate them ?
  

  ## Where does it apply
  - In a single object.
  - In a database.
  - System wide scale.


  ## How to do it wrong ...
  - Log shipping
  - Double writes
]



layout: false
.left-column[
  Summary
  ## N-Tiers
  ## C.Q.R.S.
  ## Event Sourcing
]
.right-column[
  ## Store the log, project the state
  - What is an Event ?
  - Aggregates & Streams
  - Event Store
  - Projections


  ## Magic features
  - Super specialized read models
  - Audit for free
  - Business trace for free
  - Time machine 
  - Easy to scale


  ## Can go wrong ?
  - Checkpoints / Idempotency
  - Ordering
  - Eventually consistent / Eventual consistency
  - Split brain
  - Versioning events
]



template: inverse