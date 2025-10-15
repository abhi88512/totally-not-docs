Question 1: What is useMemo in React?

        - It is a hook used to memoize the result of a function and cache it, recalculating 
        it only if the dependencies change.

Question 2: When should you use useMemo Hook?

        - When computing a value is expensive or time-consuming.
        - When you want to prevent unnecessary re-computation of values across re-renders.

Question 3: How does useMemo differ from useState?
      useMemo memoizes a computed value and returns the cached value without causing re-renders,
      while useState manages state and triggers re-renders when the state changes.

Question 4: What is useCallback in React? How is it diffrent from
        useMemo ? show with a simple example ?

        It is hook used to memoize a provided callback function, returning the memoized version
        of the function.
Question 5: What happens when you use useCallback with empty
        dependencies?

        It will return the same memoized function on every render, which might be useful 
        for performance optimization.
Question 6: When should u not use useCallback or useMemo?
        - Event Handlers or Inline Functions
        - Excessive Memory Consumption
        - Garbage Collection Concerns

