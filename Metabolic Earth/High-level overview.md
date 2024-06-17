The app is essentially a single-page PWA (progressive web app) that loads an ArcGis map view of a spinning globe. There are a few UI features - ArcGis widgets - that can interpret the different data layers loaded onto the map and e.g. make visible the map features in a legend, or toggle the data layers.

There are three main files:
1. src/index.jsx
2. src/pages/Main/index.jsx
3. src/components/ArcGis/index.jsx

The ArcGis component defines how the map is displayed and returns an article containing several divs that are to be rendered:

```jsx
// src/components/ArcGis/index.jsx
export default ({ geojson }) => {
    const mapRef = useRef()
    const [loading, setLoading] = useState(true)
    const { locale, I18n, i18n } = useI18n()

    useEffect(async () => {
	    // Ham and cheese
	    ...
    }, [locale, geojson])
    return (

        <article className="ArcGis">
            {loading && <div className="loading" />}
            <div id="logo" className="esri-widget" />
            <div className="webmap" ref={mapRef} />
        </article>
    )
}
```

The ArcGis component accepts a property called geojson, which is passed from the main page. Since everything is within the useEffect hook, the map will be updated whenever there are changes to the geojson property. 

```jsx
// stc/pages/Main/index.jsx
export default () => {
    
    useEffect(() => {
        fx.getGeolocations()
    }, [])
    
    return (
        <section className="Main">
            <header className="d-flex justify-content-between">
	            ...
            </header>
            
            <main style={{ height: resize.height }}>
                <ArcGis geojson={fx.geojson} /> // THIS BIT
            </main>
            
            <footer></footer>
        </section>
    )
}
```

This page is served by the entry-point of the app:

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