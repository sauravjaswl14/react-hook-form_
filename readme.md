## react-hook-form tutorial

Forms are a crucia aspect of any business application. As application users forms are associated with various tasks like registering, logging in, making purchases, scheduling appointments and much more.

As Application developers however forms are associated with painstaking tasks like handling form data, enforcing validation, providing visual feedback with error messages and finally data submission in a way that is both efficient and effective for the user.

## What is react-hook-form?

React hook form is a small library that helps you deal with forms in react

## Now Why would you want to use react hook form?

-Manage form data
-Submit form data
-Enforce validations
-Provide visual feedback
-React Hook Form provides a simple, scalable, and performant way to manage even the most complex of forms.

It abstracts away the tedious aspects of form management so that you can focus on creating the form itself.

## Form Setup

let's call it a youtube form. The form has 3 fields: username, email, channel, at the bottom there is a submit button to submit the form.

## npm install react-hook-form

In YoutubeForm.tsx we are going to import a hook called useForm from the react-hook-form library

import {useForm} from 'react-hook-form'

This Hook is the primary tool the library provides for managing forms with ease.

While this hook accepts an optional object as argument, it's not essential for this section on fundamentals, what's important is the object this hook returns which we will call form.

This object will also help us with the three points we have been discussing related to working with forms which are managing form data, submitting form data, and dealing with form validation and feedback.

While these points may seem repetitive it's crucial to emphasize these and understand what the library is here to accomplish.

## Managing form state

We learned about the useForm hook. This hook returns an object that contains several useful properties and methods that can be used with forms.

Now we'll dive deeper and understand how the useForm hook helps manage form state.

So What exactly do we we mean by form state? every form has a few moving parts that keep changing from the time a user loads the form to the time they submit it.

This can include:
-The current value of every field in the form
-Whether a field has been interacted with
-Whether a field's value has changed
-whether the form is invalid
-Whether a field contains errors
and much more...

All of this data collectively can be referred to as the form state

In code we can represent the form state as an object with key-value pairs

{
values: {...}
visited: {...}
errors: {...}
isValid: boolean
}

As you can see there is too much to track and trying to do this manually is time consuming.

let's understand how react-hook-form makes this process easier.

To help manage form state react-hook-form provides a method called register that can be accessed on the form object.

const form = useForm()
const {register} = form

-> this method allows us to register a form control with react-hook-form

we can call this method passing in a string argument, to register the username field we pass in username as the string.

register("username")

This method in turn returns four methods that we need to hook into the form control.

const {name, ref, onChange, onBlur} = register("username")

Now on the username input we can add props:

<input type="text" id="username" name={name} ref={ref} onChange={onChange} onBlur={onBlur} />

Doing this automatically enables react-hook-form to start tracking the state of this form control.

However this does seem like an awful lot of code to track just one field, right? well, yes but in the library's defense We've seen the elaborated version of what happens under the hood.

=> To Simplify registering a field with react-hook-form, we can directly spread the register method on the form control

const form = useForm()
const {register} = form;

<input type="text" id="username" {...register("username")} />
<input type="email" id="email" {...register("email")} />
<input type="text" id="channel" {...register("channel")} />

If you haven't noticed, the argument is nothing but the name attribute value that was previously present.

All right, react hook form is now incharge of our form state. But how exactly do we verify that?

## DevTools Visualization

We learnt about the register method in react-hook-form for tracking our form state but we didnot verify that, now we'll verify if the library is indeed managing our form state. The verification will be slightly different. Instead of verifying by writing code, we visualize the form state using the react-hook-form dev tools.

npm install -D @hookform/devtools

import the Devtool component:

import {DevTool} from '@hookform/devtools'

We then invoke the component after the closing form tag

<form>
.
.

<DevTool/>
</form>

finally we need to associate this component with the form we are tracking, for that useForm hook returns a control object that we can destructure from form.

On the devtools component we specify a control prop and assign the control object as value.

<form>
.
.
<DevTool control={control}>
</form>

we're basically tying together our YouTube form with the dev tools.

If we now head back to the browser, we should see a small icon on the top right corner of the screen.
click to open and we should see username email and channel which should seem familiar, they are the three fileds in our form.
If you expand all you will see two properties for each field: touched and dirty

touched indicates whether the field has been interacted with
dirty indicates whether the field value has changed

## Form state and Rerenders

Previously with the help of react hook form devtools, we were able to clearly see that the library is tracking the field values. What you should also know is that react hook form does this without re-rendering the component, and this is great for performance.

In traditional react forms where you worked with controlled components, every keystroke will cause the component and its children to re-render. React hook form on the other hand does not do that. It follows the uncontrolled inputs behavior. A very important point to keep in mind.

## Form Submission

Now that we know how to manage form state, let's understand how to handle form submissions with react-hook-form. The process involves three simple steps:

step-1: Define the function that should be called when the submit button is pressed

const onSubmit = () => {
console.log('Form submitted')
}

step-2: From the form object destructure a function called handleSubmit. listen to the form on submit event and assign handleSubmit as the handler. To handleSubmit, pass the onSubmit function as argument.

const {register, control, handleSubmit} = form

const onSubmit = () => {
console.log('Form submitted')
}

<form onSubmit={handleSubmit(onSubmit)}>

By doing this, the onSubmit function automatically receives access too the form data which we can log to the console

step-3 fix the typescript error that has popped up. react-hook-form requires us to define the type of form data being submitted. let's create the form values type at the top.

type FormValues = {
username: string
email: string
channel: string
}
