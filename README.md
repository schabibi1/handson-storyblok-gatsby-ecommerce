# Storyblok: Gatsby & Shopify e-commerce

This is a hands-on tutorial to build Storyblok with Gatsby & Shopify e-commerce project.

# Environment setup (follow the multilingual blog post except starter)

- Install `gatsby-cli`

```
$ npm install -g gatsby-cli
```

- Create e-commerce starter with `gatsby-shopify-starter`

```
$ gatsby new gatsby-shopify-starter https://github.com/AlexanderProd/gatsby-shopify-starter
$ cd gatsby-shopify-starter
$ gatsby develop
```

5. Check `localhost:8000`. You can see gatsby-shopify-starter is running in the browser.

# Connect Storyblok (follow the multilingual blog post)

- Sign in to Storyblok
- Click "Create new space"
- Select "Create a new space"
- Install `gatsby-source-plugin` to link Storyblok and GraphQL & Install `storyblok-react` for editor interface

```
$ npm install --save gatsby-source-storyblok storyblok-react
```

- Settings -> General Tab -> Fill **"Location (default environment)"** as **"http://localhost:8000/"**
- Settings -> General Tab -> Fill **"Preview urls"** as **"dev"** and **"http://localhost:8000"**
- Settings -> API-Keys -> Copy the preview token & paste into `gatsby-config.js` file

 `gatsby-congif.js`

```
module.exports = {
  siteMetadata: {
    title: 'Gatsby Default Starter',
  },
  plugins: [
    {
      resolve: 'gatsby-source-storyblok',
      options: {
        accessToken: 'YOUR_PREVIEW_TOKEN',
        homeSlug: 'home',
        version: process.env.NODE_ENV === 'production' ? 'published' : 'draft'
      }
    },
    ...
  ]
}
```

- Start the servert to check everything works

```
$ gatsby develop
```

# Creating Components (follow the multilingual blog post except Page component)

- Create DynamicComponent, Page, Teaser, Feature, Grid, and Placeholder components

 `components/DynamicComponent/index.js`

```javascript
import React from 'react'
import Teaser from './Teaser'
import Feature from './Feature'
import Grid from './Grid'
import Placeholder from './Placeholder'

const Components = {
  'teaser': Teaser,
  'feature': Feature,
  'grid': Grid
}

const Component = ({blok}) => {
  if (typeof Components[blok.component] !== 'undefined') {
    const Component = Components[blok.component]
    return <Component blok={blok} />
  }
  return blok.component ? <Placeholder componentName={blok.component}/> : null
}

export default Component
```

 `components/Page/index.js`

```javascript
import React from "react"
import DynamicComponent from "../DynamicComponent"
import SbEditable from 'storyblok-react'

const Page = ({ blok }) => {
  const content =
    blok.body &&
    blok.body.map(childBlok => <DynamicComponent blok={childBlok} key={childBlok._uid}/>)
  return (
    <SbEditable content={blok}>
      { content }
    </SbEditable>
  )
}

export default Page
```

 `components/Teaser/index.js`

```javascript
import React from 'react'
import SbEditable from 'storyblok-react'

const Teaser = ({blok}) => {
  return (
    <SbEditable content={blok}>
      <div>
        <h1>{blok.headline}</h1>
      </div>
    </SbEditable>
  )
}

export default Teaser
```

 `components/Grid/index.js`

```javascript
import React from 'react'
import DynamicComponent from '../DynamicComponent'
import SbEditable from 'storyblok-react'

const Grid = ({ blok }) => (
  <SbEditable content={blok} key={blok._uid}>
    <ul>
      {blok.columns.map((blok) => (
        <li key={blok._uid}>
          <DynamicComponent blok={blok} />
        </li>
      )
      )}
    </ul>
  </SbEditable>
)

export default Grid
```

 `components/Feature/index.js`

```javascript
import React from 'react'
import SbEditable from 'storyblok-react'

const Feature = ({ blok }) => {
  return (
    <SbEditable content={blok} key={blok._uid}>
      <div>
        <img src="" />
        <div>
          <div>{blok.name}</div>
          <p>
            {blok.description}
          </p>
        </div>
      </div>
    </SbEditable>
  )
}

export default Feature
```

 `components/Placeholder/index.js`

```javascript
import React from "react"

const Placeholder = ({componentName}) => (
  <div>
    <p>The component <strong>{componentName}</strong> has not been created yet.</p>
  </div>
);

export default Placeholder;
```

The steps below are the same in multilingual blog post.

# Loading the components in Gatsby

# Setting up the Storyblok Editor

# Changing the real path field

# Connecting the Storyblok Bridge

From here, we'll create more components looks like shop ovewview.

# Create ProductGrid component