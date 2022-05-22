# React Router V6 Study

This project is a study case. I'm taking a project initially created with react-router-dom V5 and converting it to V6 in order to learn how to integrate the new routing into other apps/sites.

## Version 6 - React Router

The new version of react router comes with a few improvements and breaking changes. Most notable is the way we declare routes. This changes how we do nested routes, use redirects and, we no longer have the switch component. By the end of this study, I will be able to upgrade existing React projects and incorporate v6 into new projects.


### `<Switch>` Replaced with `<Routes>`

All of our routes need to be inside a `<Routes>` component whenever we have a route we want to register.


### `<Route>` Component Handling Changed

The 'exact' prop is no longer required. It is *default* now.

How we register the jsx component for the route is different too, it is no longer nested inside opening and closing route markers. Route is now self closing and has an 'element' prop added to display the jsx component, like so:

```javascript
  <Route path="/about" element={<About />} />
```


### `<Redirect>` Changed:

In version 5, we use the `<Redirect>` component and add a `to` prop, indicating where we want to redirect.

With V6, this redirect component no longer exists. Instead, we need to use the `<Navigate>` component

```javascript
  <Route path="/redirect" element={<Navigate to="/about" />}/>
```


### Conditional Redirects

Conditional Redirects are great for when you have a website with an authentication system (protected routes). They allows you to check a users status (logged-in or not) and redirect them according to their status.

Another great use case for React Routers conditional redirects is an eCommerce site. In the example below, the user is redirected to the products page component if they have no items in their shopping cart.

```javascript
  <Route
    path="/checkout"
    element={
      isCartEmpty
      ? <Navigate to="/products" />
      : <p>Congrats! You successfully made it to checkout. </p> }/>
```


### How to Programmatically Redirect User

In V5, we use the `useHistory()` hook to programmatically redirect the user. In V6, we use the `useNavigate()` hook instead. *Note:* the new `<Navigate>` component is different then the `useNavigate()` hook.

   Version 5:

```javascript
   <button onClick={() => history.push('/products') }>See our products</button>
```

   Version 6:

```javascript
   <button onClick={() => navigate('/products') }>See our products</button>
```


### Route Nesting

In version 6, when you want to nest a route (or multiples), they need to be wrapped in a `<Routes>` component and need to be configured. The `<Route />` component is self closing in v6 and uses the element prop for the jsx.

   Version 5:

```javascript
  <Route path="/about/offers">
    <Offers />
  </Route>
```

   Version 6:

```javascript
  <Routes>
    <Route path="offers" element={<Offers />} />
  </Routes>
```

Plus, nested route paths automatically become relative to the parent path that they are used in. So we can remove the `/about/` from the path.

We also need to update the `about` path inside the *root component* because it is 'exact match' by default now. You just need to add an *asterix* (wildcard character) after the about part in the route path. 

Version 5:
```javascript
<Route path="/about" element={<About />} />
```

In V6 becomes:
```javascript
<Route path="/about/*" element={<About />} />
```


### Mutable Route Nesting

With mutable paths (`${path}/offers`), where a changeable path is needed, we used the `useRouteMatch()` hook in version 5. In version 6, working with mutable paths is much easier because nested route paths are automatically relative to their parent. We no longer need to use a hook.

We also need to update the path in the *root component* to have an *asterix* just like for immutable nested routes.

Version 5:

```javascript
<Route path={`${path}/offers`}>
  <Offers />
</Route>
```

Version 6:

```javascript
<Routes>
  <Route path={`offers`} element={<Offers />} />
</Routes>
```


