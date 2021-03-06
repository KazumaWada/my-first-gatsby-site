<p align="center">
  <a href="https://www.gatsbyjs.com/?utm_source=starter&utm_medium=readme&utm_campaign=minimal-starter">
    <img alt="Gatsby" src="https://www.gatsbyjs.com/Gatsby-Monogram.svg" width="60" />
  </a>
</p>
<h1 align="center">
  Gatsby minimal starter
</h1>

## ๐ Quick start

1.  **Create a Gatsby site.**

    Use the Gatsby CLI to create a new site, specifying the minimal starter.

    ```shell
    # create a new Gatsby site using the minimal starter
    npm init gatsby
    ```

2.  **Start developing.**

    Navigate into your new siteโs directory and start it up.

    ```shell
    cd my-gatsby-site/
    npm run develop
    ```

3.  **Open the code and start customizing!**

    Your site is now running at http://localhost:8000!

    Edit `src/pages/index.js` to see your site update in real-time!

4.  **Learn more**

    - [Documentation](https://www.gatsbyjs.com/docs/?utm_source=starter&utm_medium=readme&utm_campaign=minimal-starter)

    - [Tutorials](https://www.gatsbyjs.com/tutorial/?utm_source=starter&utm_medium=readme&utm_campaign=minimal-starter)

    - [Guides](https://www.gatsbyjs.com/tutorial/?utm_source=starter&utm_medium=readme&utm_campaign=minimal-starter)

    - [API Reference](https://www.gatsbyjs.com/docs/api-reference/?utm_source=starter&utm_medium=readme&utm_campaign=minimal-starter)

    - [Plugin Library](https://www.gatsbyjs.com/plugins?utm_source=starter&utm_medium=readme&utm_campaign=minimal-starter)

    - [Cheat Sheet](https://www.gatsbyjs.com/docs/cheat-sheet/?utm_source=starter&utm_medium=readme&utm_campaign=minimal-starter)

## ๐ Quick start (Gatsby Cloud)

Deploy this starter with one click on [Gatsby Cloud](https://www.gatsbyjs.com/cloud/):

[<img src="https://www.gatsbyjs.com/deploynow.svg" alt="Deploy to Gatsby Cloud">](https://www.gatsbyjs.com/dashboard/deploynow?url=https://github.com/gatsbyjs/gatsby-starter-minimal)

# what i learned so far

## ใชใใใใใใใ?

ใพใ่ชๅใฎใดใผใซใฏใ**gatsby ใๆใ้ใใซใขใฌใณใธใงใใใใจ**ใ่ชๅใฎๆบ่ถณใใ web ใตใคใใไฝใใใจใ

JavaScript ใฎใใฅใผใใชใขใซใซ้ฃฝใใฆใReact ใธ็งปใใๆใฃใใใฉใใใฎใใฅใผใใชใขใซใใใพใใพ่ฆใคใใฆใReact ใจ Gatsby ใๅๆใซๅญฆ็ฟใงใใใใ่ฏใใ?ใใใจๆใฃใใ

## ใใฃใฆใฟใ

[Part 1: Create and Deploy Your First Gatsby Site](https://www.gatsbyjs.com/docs/tutorial/part-1/)

ๅใใฆใฎ React ใใคใณใ 3 ใค

- import ใใ
- jsx ใใ
- export ใใ

```jsx
// Step 1: Import React. This lets you use JSX inside your .js file.
import * as React from "react";

/* Step 2: Define your component. Note that your
component name should start with a capital letter. */
const MyComponent = () => {
  return <h1>Hi, welcome to my site!</h1>;
};

/* Step 3: Export your component so it
can be used by other parts of your app. */
export default MyComponent;
```

## Props ใฎใใใใง Dinamic ใซใชใไบใใงใใ

ใใพใใก็่งฃใใฆใใชใใใฉใiceCreamFlavor="mint chip"ใฃใฆใใใใใผใญใใจใใใฃใใใใใฎใณใณใใผใใณใๅใง props.iceCreamFlavor ใไฝฟใใใฃใฆไบใใช?

CSS ใฏ้จๅๅไฝใงๅผใณๅบใไบใใงใใ

```jsx
.title {
  color: blue;
  font-size: 3rem;
}

---

import * as React from 'react'
import { title } from './my-component.module.css'
const MyComponent = () => {
  return (
    <h1 className={title}>
      Super Sweet Title Page
    </h1>
  )
}
export default MyComponent
```

ใใใใๅผใณๅบใใใๆใฏใ

```jsx
import {
  container,
  heading,
  navLinks,
  navLinkItem,
  navLinkText,
} from "./layout.module.css";
```

npm ใง plugin ใใคใณในใใผใซใใไบใใงใใใ

## How to pull data from GraphiQL

it looks same as REST

```jsx
import * as React from "react";
// Step 1: Import the useStaticQuery hook and graphql tag
import { useStaticQuery, graphql } from "gatsby";
const Header = () => {
  /* Step 2: Use the useStaticQuery hook and
    graphql tag to query for data
    (The query gets run at build time) */
  const data = useStaticQuery(graphql`
    query {
      site {
        siteMetadata {
          title
        }
      }
    }
  `);
  return (
    <header>
      {/* Step 3: Use the data in your component */}
      <h1>{data.site.siteMetadata.title}</h1>
    </header>
  );
};
export default Header;
```

## GraqhiQL more in detail

![](https://www.gatsbyjs.com/static/04384c192391ebeac3b63ea42872f3f2/7970d/data-layer-with-nodes.png)

- ็ใไธญใฎ็ฎๆใซ่ฟฝๅ?ใใใใใผใฟใๅฅๅใใฆ play ใใฟใณใๆผใใใใๅฎ้ใซ ๅณๅดใฎ json ใซ่ฟฝๅ?ใใใใmodel ใจใไฝใใชใใฆ่ฏใใใ็ฐกๅ!ใพใใๆฅไป้?ใชใฉใซไธฆใณๆฟใใใๆใๅๆงใซ็ใไธญใซๆธใใฆใๆฌฒใใ json ใไฝใไบใใงใใใ

```json
query MyQuery {
  allMdx(sort: {fields: frontmatter___date, order: DESC}) {
    nodes {
      frontmatter {
        date(formatString: "MMMM D, YYYY")
        title
      }
      id
      body
    }
  }
}

```

- ใชใใใกใคใซๅใ{MDXRenderer.slug}.js ใชใฎใใ
  {
  "data": {
  "allMdx": {
  "nodes": [
  {
  "slug": "another-post"
  },
  {
  "slug": "my-first-post"
  },
  {
  "slug": "yet-another-post"
  }
  ]
  }
  },
  "extensions": {}
  }

  {MDXRenderer.slug}.js ใจใใใใจใงใใฟใคใใซๅ.js ใซใชใใ->pages ใใฉใซใใฏๅจ้จใใกใคใซๅใใใฎใพใพ/ใใกใคใซๅใซใชใใใใใใ(index.js ใ?ใจ่ชๅ็ใซ root ใซใชใใฃใฝใ)

## query variables (ๆ็จฟใฎ id ใ QL ใซๅใใใใฆใ็นๅฎใฎๆ็จฟใ pull ใใ)

```javascript
import * as React from "react";
import { graphql } from "gatsby";
import { MDXRenderer } from "gatsby-plugin-mdx";

const BlogPost = ({ data }) => {
  return (
    <Layout pageTitle={data.mdx.frontmatter.title}>
      <p>{data.mdx.frontmatter.date}</p>
      <MDXRenderer>{data.mdx.body}</MDXRenderer>
    </Layout>
  );
};

export const query = graphql`
  query ($id: String) {
    mdx(id: { eq: $id }) {
      frontmatter {
        title
        date(formatString: "MMMM D, YYYY")
      }
      body
    }
  }
`;
```

## ใชใใจใชใใใใฃใฆใใใ

ใใผใฟใ GraohiQL ใซ่ฟฝๅ?ใใใ GraphiQL ใใๆฌฒใใใใผใฟใใจใฃใฆใใฆใใใฎใณใผใใ js ใใกใคใซใซๆธใใฆใๅคๆฐใซๆ?ผ็ดใใฆใhtml ใซใใ(ๅคๆฐ)ใๅฅๅใใใใใฃใฆใใใจใฏ Rails,MysQL ใงใ REST ใงใไธ็ทใ

## blog post does loop

```javascript
{
  data.allMdx.nodes.map((node) => (
    <article key={node.id}>
      <h2>
        <Link to={`/blog/${node.slug}`}>{node.frontmatter.title}</Link>
      </h2>
      <p>Posted: {node.frontmatter.date}</p>
    </article>
  ));
}

export const query = graphql`
  query {
    allMdx(sort: { fields: frontmatter___date, order: DESC }) {
      nodes {
        frontmatter {
          date(formatString: "MMMM D, YYYY")
          title
        }
        id
        slug
      }
    }
  }
`;
```

## frontmatter ใซ้?็ฎใ่ฟฝๅ?ใใฆใgatsby develop ใใชในใฟใผใใใใใฐใGraphiQL ใซ้?็ฎใ่ฟฝๅ?ใใใฆใใใ
