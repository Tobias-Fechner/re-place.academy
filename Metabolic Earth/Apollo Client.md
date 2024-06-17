# Apollo Client Setup
Role of Apollo Client

- **Data Fetching**: The Apollo Client is responsible for fetching data from your GraphQL server. Components wrapped by `ApolloProvider` can use hooks like `useQuery` and `useMutation` to send queries and mutations to the server.
- **State Management**: It also helps manage the state of your application by caching query results and allowing components to reactively update when data changes.
- **Network Management**: The Apollo Client handles the network layer, managing requests and responses between your app and the GraphQL server, and handling errors and retries.

```jsx
const apolloClient = new ApolloClient({
  cache: new InMemoryCache(),
  link: new HttpLink({ uri: import.meta.env.VITE_API_REGENERATI_BE_GRAPHQL }),
  defaultOptions: {
    watchQuery: {
      fetchPolicy: 'no-cache'
    },
    query: {
      fetchPolicy: 'no-cache'
    }
  },
  connectToDevTools: false
})

```
# Apollo Provider
An Apollo provider is used to wrap the main component of the web app. That way, Apollo Client is available in the rest of the react component tree. 

```jsx
render(
  <ApolloProvider client={apolloClient}>
    <I18nProvider value={i18nYML}>
      <MainPage />
    </I18nProvider>
  </ApolloProvider>,
  document.getElementById('root')
)

```
# Summary with Code Snippets
1. **Apollo Client Setup**:
   - `const apolloClient = new ApolloClient(...)`: Initializes Apollo Client with caching, link to the GraphQL server, and fetch policies.

2. **Rendering the Main Page**:
   - `render(...)`: Renders the main application wrapped in ApolloProvider and I18nProvider to manage data fetching and translations.

3. **ApolloProvider**:
   - `<ApolloProvider client={apolloClient}>`: Wraps the app to provide the Apollo Client to all components, enabling GraphQL queries and mutations.

4. **I18nProvider**:
   - `<I18nProvider value={i18nYML}>`: Supplies internationalization settings to components for rendering text in different languages.

5. **MainPage Component**:
   - `<MainPage />`: The main component that gets rendered, containing the core UI of the application.

6. **Data Fetching Example**:
   - `const { loading, error, data } = useQuery(GET_DATA);`: Uses Apollo Client’s `useQuery` hook to fetch data from the GraphQL server and handle loading, errors, and results.