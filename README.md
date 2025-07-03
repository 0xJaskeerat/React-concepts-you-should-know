# React-concepts-you-should-know

### What is Rendering ? How React performs rendering ?
We as devs create a Component ( Class / Functional ) and import it something like :

```
 <SubmitModal size="md" />
```

React here takes the component instance and checks that if this can be translated to actual Browser DOM --> and that's what user sees on the browser

Process:
1. React creates element definition of each of the component with 4 Key Properties --> Type, Props, Ref, Key


Example: 
```
  <DeleteProfile>
    <Text>Delete Profile ?</Text>
    <Button variant="primary">Cancel</Button>
    <Button variant="danger">Delete</Button>
  <DeleteProfile>

```

is perceived as 

```
const DeleteProfile = () => ({
    type: 'div',
    props: {
        children: [
            {
                type: 'p',
                props: {
                    children: 'Delete profile ? '
                }
            },
            {
                type: 'button',
                props: {
                    color: 'blue',
                    children: 'Cancel'
                }
            }, 
            {
                type: 'button',
                props: {
                    color: 'red',
                    children: 'Delete'
                }
            }
        ]
    }
})

```

But constructing the DOM everytime may not be the best solution , hence react comes with famous optimization techniques like <code>Virtual DOM</code> , <code>Reconciliation Algorithm</code>

* Rendering --> Process of converting the code into Equivalent DOM ( involves React doing optimization techniques to update the Virtual DOM and eventually the DOM for the user to see )
* Note: React itself can't render on the browser , hence use <code>ReactDOM</code> , since React doesn't know what to do with the tree of elements ( see above ) , that's the reason we are able to use that in mobile apps as well 
* 'React' named coz it reacts to the changes and keeps UI in sync

React doesn't understand HTML / JSX , it's all just Javascript 
and that's the reason you can inject React and ReactDOM in a plain HTML document as well

Check this out
```
function DeleteProfile () {
    const [isDeleted, setIsDeleted] = React.useState(false);
    
    if(isDeleted){
        return React.createElement("h1", null, "Sorry, bad request")
    }else{
        return React.createElement(
            "button", 
            {
                onClick: () => setIsDeleted(true)
            },
            "Delete"
        )
    }
}

const domContainer = document.querySelector("#delete-modal");
const root = ReactDOM.createRoot(domContainer)
root.render(React.createElement(DeleteProfile))
    

```

To use JSX, tools like Babel are used and bundlers which bundle your JS Code 
Create React App --> this was something created by React team that allowed you to scaffold a React project with all these set up
Also React is a library , so we can come up with out own Toolchain --> Vite , Next.js etc.


React is <code>Declarative</code> instead of <code>Imperative</code> , which means React doesn't direclty interact with the DOM like appending HTML elements
For that , we have <code>JSX</code> --> Java Script XML , which let's you write HTML write syntax
But, but React doesn't understand JSX, so we need tools like <code>Babel</code> 


### How React updates the DOM ? 

Simple 3 steps involved:
1. Trigger : 
2. Render :
3. Commit :


### Why does a React component re-render after the first render? Do we really need re-rendering
--> Simple answer to why we need re-rendering : To avoid static webapge similar to Earlier internet days

The answer most of us give when asked : When does a React component re-render
---> Whenever state changes or props passed to it change

Now this answer may look logically correct but is in-accurate

First things first, we need to understand when a Parent component re-renders , all children components re-render as well
Reason: React assumes all the components are not pure, so to not take any chances React re-renders all the children components as well
Eg: A child component may be calling an API [ which is a sort of side-effect ] 

The information doesn't mean that the DOM is created from scratch again and again everytime something happens, coz we have really beautiful Optimizations present --> Reconciliation Algorithm, which detects the bare-minimum changes to be made to the actual DOM via Virtual DOM

#### Note: If you still want your child component to not re-render un-necessarily , then maybe make wrap the component with React.memo, which simply tells React that O/P of these component simply depends on props it receives


Finally , we understood 
Component re-renders when its state changes and it triggers a re-render on all its child component, the rendering is itself an optimised process coz of Reconciliation but still we can handle that using React.memo









