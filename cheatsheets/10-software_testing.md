# Software Testing

## Coverage Criteria

  - **Test Requirement**
    - A test requirement is a specific element of a software artifact that a test case must satisfy or cover.
  - **Coverage Criterion**
    - A coverage criterion is a rule or collection of rules that impose test requirements on a test set.
  - **Coverage**
    - Given a set of test requirements `TR` for a coverage criterion `C`,
      - a test set `T` satisfies `C` if and only if for every test requirement `tr` in `TR`, at least one test `t` in `T` exists such that `t` satisfies `tr`.
  - **Coverage Level**
    - Given a set of test requirements `TR` and a test set `T`,
      - the coverage level is simply the ratio of the number of test requirements satisfied by `T` to the size of `TR`.


## V-Model

  - Unit Testing         —>  Implementation/Code
  - Component Testing    —>  Detailed Design
  - Integration Testing  —>  Subsystem Design
  - System Testing       —>  Architectural Design
  - Acceptance Testing   —>  Requirements


## Testing Pyramid

  - E2E Testing
  - Integration Testing
  - Component Testing
  - Unit Testing

## Misc

### API Testing

### UI Testing

### Performance Testing

  - Load Testing
  - Stress Testing
  - Spike Testing
  - Endurance Testing
  - Scalability testing
