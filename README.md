# Frontend Mentor - Multi-step form solution

This is a solution to the [Multi-step form challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/multistep-form-YVAnSdqQBJ). 

## Overview

### The challenge

Users should be able to:

- Complete each step of the sequence
- See a summary of their selections on the final step and confirm their order
- View the optimal layout for the interface depending on their device's screen size
- See hover and focus states for all interactive elements on the page

### Screenshot

![](./screenshot.jpg)

### Links

- Solution URL: [Github](https://github.com/jeremylloyd/frontend-mentor-multi-step-form)
- Live Site URL: [Vercel](https://frontend-mentor-multi-step-form.vercel.app/)

## My process

### Built with

- HTML5
- CSS (BEM)
- JS
- Svelte

### What I learned

- Using components in Svelte
  - Make each page it's own component for complex websites. If you don't, your HTML becomes very long and hard to maintain.
  - Setting the `on:click` property of a component won't work unless you also add the `on:click` property inside the Svelte component (i.e. 'passing' the signal up and down the hierarchy)
  - Designing components for reusability
    - Don't embed responsive media queries for small components like buttons. Instead, change the component style at the top-level (which will have more context)
    - Keep all the components you want to reuse in one place and well organised
- General workflow
  - Don't worry about perfecting margins and padding until you've got the responsive layout working
  - Be disciplined in focusing on getting one component done at a time before moving onto the next
- HTML
  - The default behaviour for validating text inputs when submitting forms is pretty useful. If you want to use it (which you can just override with `preventDefault` in JS if necessary)
