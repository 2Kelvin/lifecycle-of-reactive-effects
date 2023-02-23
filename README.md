# lifecycle-of-reactive-effects

In this read, I learnt:

- `an Effect has only 2 lifecycles`:
  - [x] Syncronizing with an external system/network
  - [x] Stopping the synchronization with the external system
- _these is the only pair cycle (start synchronization & stop synchronization) to focus on when you're creating an Effect_
- useEffect's lifecycle is dependent (i.e how many times wil it rerun/ resynchronize) on the items you put inside the dependency array (which is dependent on the state/props you use in the effect). Therefore, the Effect's lifecyle is dependent on when it'll fire again if the props/state in the dependency aray change
- `each effect should perform one specific task, one separate synchronization process` e.g. use two separate useEffects to fetch data & send analytics
- `useEffect reacts to reactive values`. If a variable in useEffect never changes, then it doesn't need to be put in the dependency array since it won't trigger any resynchronizations or new Effect lifecycles. `Effects use state & props as dependencies` since they can change at any time of react's data flow
- **regular variables cannot be put in useEffect's dependency array since they do not change. State variables however can because they change cause rerenders**
- **always include a cleanup function to your Effect even if it doesn't rely on any dependencies**. Don't think from the component's perspective of mounting, updating & unmounting, **think from the Effect's perspective of its 2 lifecycles.** This way if the variables in useEffect suddenly become reactive, the code in the Effect won't change, all you'll have to do is add the reactive variables as dependencies to the Effect
- any variable that's a result of calculating two or more state or props is reactive and should be included as a dependency if used in useEffect. This is because, if the respective state/prop change, ultimately the calculated variables will too after the rerender
- **all variables from a component's body used by useEffect should be in the list of dependencies since they're reactive**
- `Effect's react to all variables in a component's body`
- values/ variables that mutate cannot be dependencies and are not considered reactive since they are impure and cannot cause a rerender due to react not being able to track them e.g. a ref
- **react's linter** will always pop up in your console when you forget to add a reactive value you used in your Effect to the dependency array
- to make an Effect not syncronize due to a dependency, **move the dependency out of the component**. This works because they're not at any point calculated during the component rendering
- `Effects are reactive blocks of code` that resynchronize when any of their dependencies change
- You can't choose your dependencies. **Every reactive value used in an Effect MUST be included int the dependency array**
- **Avoid relying on objects & functions as dependencies** since they'll always be different after every render
