---
layout: post
title:  "Client Side Rendering (SSR) Web components"
summary: "Client Side Rendering (SSR) Web components"
author: spradeep
date: '2024-3-20 14:35:23 +0530'
category: Client Side Rendering, CSR, Web Component, HTML Web Component, Javascript Web Component
keywords: CSR, Client Side Rendering, web component, create web component, javascript, Web component 
permalink: /blog/client-side-rendering-ssr-technique-github-page/
usemathjax: true
---

# Server Side Rendering web components:

 <img src="/assets/img/posts/client-side-rendering-web-components.png" class="img-fluid">
 
## Web components:

Web Components are a set of web platform APIs that allow you to create reusable custom elements with encapsulated functionality. They are a collection of technologies that can be used together to create reusable, encapsulated, and interoperable HTML elements. These components can be used in web applications without the need for any additional frameworks or libraries.
  

## Client Side Rendering:

Client Side Rendering (CSR) is a web development approach where the bulk of the page rendering process is handled by the client's browser using JavaScript. In CSR, the server typically sends a minimal HTML document, and then JavaScript code is executed in the browser to dynamically generate and render the content.
  

## Express JS:

Fast, unopinionated, minimalist web framework for Node.js  
 

## Sample Web component

    <!DOCTYPE html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Web Components | CSR (Client side rendering Webcomponents, Needs Javascript)</title>
    </head>
    <body>
    <custom-paragraph text="Custom Paragraph"></custom-paragraph>
    </body>
    <script>
    class CustomParagraph extends HTMLElement {
    template = document.createElement("template");
    constructor() {
    super();
    const text = this.getAttribute('text');
    this.attachShadow({ mode: "open" });
    this.template.innerHTML = `
    <style>
    p {
    font-size: 65px;
    font-weight: 400;
    font-style: italic;
    background-image: linear-gradient(to left, #007f4c, #53e3a7);
    color: black;
    }
    </style>
    <p>${text}</p>
    `;
    this.render();
    }
    render() {
    this.shadowRoot.appendChild(this.template.content.cloneNode(true));
    }
    }
    customElements.define("custom-paragraph", CustomParagraph);
    </script>
    </html>
(https://github.com/pradeepin2/web-components-client-side-rendering/blob/main/csr.html)[https://github.com/pradeepin2/web-components-client-side-rendering/blob/main/csr.html]
  

## Rendering Webcomponents in Client served via Express JS:


    const express = require("express");
    const fs = require('fs');
    const app = express();
    const port = 3000;
    const content = fs.readFileSync("./csr.html","utf-8").toString();
    app.get("/csr", async(req,res) => {
    res.send(content);
    });
    app.listen(port, ()=>{
    console.log(`Example Client side rendering Webcomponents running on ${port}`);
    });
    app.listen(port, ()=>{
    console.log(`Example Server side app running on: ${port}`);
    });
(https://github.com/pradeepin2/web-components-client-side-rendering/blob/main/csr.js)[https://github.com/pradeepin2/web-components-client-side-rendering/blob/main/csr.js]
  
 ### Code Reference:
 (https://github.com/pradeepin2/web-components-client-side-rendering)[https://github.com/pradeepin2/web-components-server-side-rendering/tree/main]

  
This post can be read along with Server side rendering web components post. To get a good picture of difference between client side rendering and server side rendering 