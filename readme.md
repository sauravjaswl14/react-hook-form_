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
