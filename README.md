<p align="center">
  <a href="https://www.gatsbyjs.com/?utm_source=starter&utm_medium=readme&utm_campaign=minimal-starter">
    <img alt="Gatsby" src="https://www.gatsbyjs.com/Gatsby-Monogram.svg" width="60" />
  </a>
</p>
<h1 align="center">
  Gatsby minimal starter
</h1>

## 🚀 Quick start

1.  **Create a Gatsby site.**

    Use the Gatsby CLI to create a new site, specifying the minimal starter.

    ```shell
    # create a new Gatsby site using the minimal starter
    npm init gatsby
    ```

2.  **Start developing.**

    Navigate into your new site’s directory and start it up.

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

## 🚀 Quick start (Gatsby Cloud)

Deploy this starter with one click on [Gatsby Cloud](https://www.gatsbyjs.com/cloud/):

[<img src="https://www.gatsbyjs.com/deploynow.svg" alt="Deploy to Gatsby Cloud">](https://www.gatsbyjs.com/dashboard/deploynow?url=https://github.com/gatsbyjs/gatsby-starter-minimal)

# what i learned so far

## なぜこれをやるか?

まず自分のゴールは、**gatsby を思い通りにアレンジできること**。自分の満足する web サイトを作ること。

JavaScript のチュートリアルに飽きて、React へ移ろう思ったけど、このチュートリアルをたまたま見つけて、React と Gatsby を同時に学習できるから良いだろうと思った。

## やってみる

[Part 1: Create and Deploy Your First Gatsby Site](https://www.gatsbyjs.com/docs/tutorial/part-1/)

初めての React ポイント 3 つ

- import する
- jsx する
- export する

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

## Props のおかげで Dinamic になる事ができる

いまいち理解していないけど、iceCreamFlavor="mint chip"ってこんんポーねんとがあったら、そのコンポーネント内で props.iceCreamFlavor が使えるって事かな?

CSS は部品単体で呼び出す事ができる

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

たくさん呼び出したい時は、

```jsx
import {
  container,
  heading,
  navLinks,
  navLinkItem,
  navLinkText,
} from "./layout.module.css";
```

npm で plugin をインストールする事ができる。

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

- 真ん中の箇所に追加したいデータを入力して play ボタンを押したら、実際に 右側の json に追加される。model とか作らなくて良いから簡単!また、日付順などに並び替えたい時も同様に真ん中に書いて、欲しい json を作る事ができる。

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

- なぜファイル名が{MDXRenderer.slug}.js なのか。
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

  {MDXRenderer.slug}.js とすることで、タイトル名.js になる。->pages フォルダは全部ファイル名がそのまま/ファイル名になるから、、、(index.js だと自動的に root になるっぽい)

## query variables (投稿の id を QL に分からせて、特定の投稿を pull する)

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

## なんとなくわかってきた。

データを GraohiQL に追加したり GraphiQL から欲しいデータをとってきて、そのコードを js ファイルに書いて、変数に格納して、html にそれ(変数)を入力する。やってることは Rails,MysQL でも REST でも一緒。

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
