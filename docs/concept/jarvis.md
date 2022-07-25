Optimizations and forecasting is two of most import features in **MOF**. Jarvis interface is used to implement different versions of AI algorithms.

## Jarvis interface
```go
type Jarvis interface {
	UnusedResource(meta *base.ReqMeta, clue *UnusedClue) (*UnusedDecision, error)

	RightSizingResource(meta *base.ReqMeta, clue *RightSizingClue) (*RightSizingDecision, error)
}
```

### Unused
**MOF** determines whether a resource is unused or not based on different resource types.

For example, for AWS EC2, bellow conditions will be checked:

- Instance state
- Instance usage metrics with threshold

### RightSizing
**MOF** determines whether a resource needs to right sized on different resource types and algorithm.

For example, for AWS EC2, bellow conditions will be checked:

- Instance usage metrics with threshold
- Instance price

!!! tip "Algorithms will be smarter!"

    - We will implement smarter algorithms in future release

### Architecture (TODO)

### Others (TODO)