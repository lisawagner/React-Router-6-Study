# React Router V6 Study

This project is a study case. I'm taking a project created with react-router-dom V5 and converting it to V6 in order to learn how to integrate the new routing into my other apps/sites.

## Version 6 - React Router

The new version or React Router comes with a few improvements and breaking changes. The most notable is the way we declare routes. This changes how we do nested routes, use redirects and, we no longer have the switch compnent. By the end of this study, I plan to be able to comfortable upgrade existing React projects and incorporate v6 into new projects.

### `<Switch>` is replaced with `<Routes>`

All of our routes need to be inside a `<Routes>` component whenever we have a route we want to register.

### `<Route>` components handling change

The 'exact' prop is no longer required. It's default now.

How we register the jsx component for the route is different too, it is no longer nested inside opening and closing route markers. Route is now self closing and has an 'element' prop added to display the jsx component, like so:

```javascript
<Route path="/about" element={<About />} />
```

