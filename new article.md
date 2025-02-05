"Skip to content
TkDodo's blog

BlogTagsSponsorsRss
BlueskyGithub
Avoiding useEffect with callback refs
14.08.2022 — ReactJs, JavaScript, TypeScript — 3 min read


Photo by Annie Spratt
#1: Avoiding useEffect with callback refs
#2: Ref Callbacks, React 19 and the Compiler
한국어
日本語
Add translation
Last Update: 2024-12-08

Note: This article assumes a basic understanding of what refs are in React.

Even though refs are mutable containers where we can theoretically store arbitrary values, they are most often used to get access to a DOM node:

a-basic-ref
Copya-basic-ref: copy code to clipboard
const ref = React.useRef(null)

return <input ref={ref} defaultValue="Hello world" />
ref is a reserved property on build-in primitives, where React will store the DOM node after it was rendered. It will be set back to null when the component is unmounted.

Interacting with refs
For most interactions, you don't need to access the underlying DOM node, because React will handle updates for us automatically. A good example where you might need a ref is focus management.

There's a good RFC from Devon Govett that proposes adding FocusManagement to react-dom, but right now, there is nothing in React that will help us with that.

Focus with an effect
So how would you, right now, focus an input element after it rendered? (I know autofocus exists, this is an example. If this bothers you, imagine you'd want to animate the node instead.)

Well, most code I've seen tries to do this:

focus-an-input
Copyfocus-an-input: copy code to clipboard
const ref = React.useRef(null)

React.useEffect(() => {
  ref.current?.focus()
}, [])

return <input ref={ref} defaultValue="Hello world" />
This is mostly fine and doesn't violate any rules. The empty dependency array is okay because the only thing used inside is the ref, which is stable. The linter won't complain about adding it to the dependency array, and the ref is also not read during render (which might be troublesome with concurrent React features).

The effect will run once "on mount" (twice in strict mode). By that time, React has already populated the ref with the DOM node, so we can focus it.

Yet this is not the best way to do it and does have some caveats in some more advanced situations.

Specifically, it assumes that the ref is "filled" when the effect runs. If it's not available, e.g. because you pass the ref to a custom component which will defer the rendering or only show the input after some other user interaction, the content of the ref will still be null when the effect runs and nothing will be focussed:

custom-form
Copycustom-form: copy code to clipboard
function App() {
  const ref = React.useRef(null)

  React.useEffect(() => {
    // 🚨 ref.current is always null when this runs
    ref.current?.focus()
  }, [])

  return <Form ref={ref} />
}

const Form = React.forwardRef((props, ref) => {
  const [show, setShow] = React.useState(false)

  return (
    <form>
      <button type="button" onClick={() => setShow(true)}>
        show
      </button>
      // 🧐 ref is attached to the input, but it's conditionally rendered
      // so it won't be filled when the above effect runs
      {show && <input ref={ref} />}
    </form>
  )
})
Here is what happens:

Form renders.
input is not rendered, ref is still null.
effect runs, does nothing.
input is shown, ref will be filled, but will not be focussed because effect won't run again.
The problem is that the effect is "bound" to the render function of the Form, while we actually want to express: "Focus the input when the input is rendered", not "when the form mounts".

Callback refs
This is where callback refs come into play. If you've ever looked at the type declarations for refs, we can see that we can not only pass a ref object into it, but also a function:

Copycopy code to clipboard
type Ref<T> = RefCallback<T> | RefObject<T> | null
Conceptually, I like to think about refs on React elements as functions that are called after the component has rendered. This function gets the rendered DOM node passed as argument. If the React element unmounts, it will be called once more with null.

Passing a ref from useRef (a RefObject) to a React element is therefore just syntactic sugar for:

callback-ref
Copycallback-ref: copy code to clipboard
<input
  ref={(node) => {
    ref.current = node;
  }}
  defaultValue="Hello world"
/>
Let me emphasize this once more:

All ref props are just functions!
And those functions run after rendering, where it is totally fine to execute side effects. Maybe it would have been better if ref would just be called onAfterRender or something.

With that knowledge, what stops us from focussing the input right inside the callback ref, where we have direct access to the node?

focus-with-callback-ref
Copyfocus-with-callback-ref: copy code to clipboard
<input
  ref={(node) => {
    node?.focus()
  }}
  defaultValue="Hello world"
/>
Well, a tiny detail does: React will run this function after every render. So unless we are fine with focussing our input that often (which we are likely not), we have to tell React to only run this when we want to.

useCallback to the rescue
Update
My view on using useCallback for those situations has changed a bit. I'll keep this post as it is for posterity, but please read #2: Ref Callbacks, React 19 and the Compiler to get the full picture.

Luckily, React uses referential stability to check if the callback ref should be run or not. That means if we pass the same ref(erence, pun intended) to it, execution will be skipped.

And that is where useCallback comes in, because that is how we ensure a function is not needlessly created. Maybe that's why they are called callback-refs - because you have to wrap them in useCallback all the time. 😂

Here's the final solution:

callback-ref-with-use-callback
Copycallback-ref-with-use-callback: copy code to clipboard
const ref = React.useCallback((node) => {
  node?.focus()
}, [])

return <input ref={ref} defaultValue="Hello world" />
Comparing this to the initial version, it's less code and only uses one hook instead of two. Also, it will work in all situations because the callback ref is bound to the lifecycle of the DOM node, not of the component that mounts it. Further, it will not execute twice in strict mode (when running in the development environment), which seems to be important to many.

And as shown in this hidden gem in the (old) React docs, you can use it to run any sort of side effects, e.g. call setState in it. I'll just leave the example here because it's actually pretty good:

measure-a-dom-node
Copymeasure-a-dom-node: copy code to clipboard
function MeasureExample() {
  const [height, setHeight] = React.useState(0)

  const measuredRef = React.useCallback(node => {
    if (node !== null) {
      setHeight(node.getBoundingClientRect().height)
    }
  }, [])

  return (
    <>
      <h1 ref={measuredRef}>Hello, world</h1>
      <h2>The above header is {Math.round(height)}px tall</h2>
    </>
  )
}
So please, if you need to interact with DOM nodes directly after they rendered, try not to jump to useRef + useEffect directly, but consider using callback refs instead.

That's it for today. Feel free to reach out to me on bluesky if you have any questions, or just leave a comment below. ⬇️

Like the monospace font in the code blocks?
Check out monolisa.dev



© 2025 by TkDodo's blog. All rights reserved.
Theme by LekoArts
"
 https://tkdodo.eu/blog/avoiding-use-effect-with-callback-refs#:~:text=Skip%20to%20content,Theme%20by%20LekoArts