---
layout: post
title:  "Server Side Rendering (SSR) Web components"
summary: "Server Side Rendering (SSR) Web components"
author: spradeep
date: '2024-3-13 14:35:23 +0530'
category: Server Side Rendering, SSR, Web Component, HTML Web Component, Javascript Web Component
keywords: SSR, Server Side Rendering, web component, create web component, javascript, Web component 
permalink: /blog/server-side-rendering-ssr-technique-github-page/
usemathjax: true
---

 <img src="/assets/img/posts/server-side-rendering-web-components.png" class="img-fluid">
 
## Web components:
 
Web Components are a set of web platform APIs that allow you to create reusable custom elements with encapsulated functionality. They are a collection of technologies that can be used together to create reusable, encapsulated, and interoperable HTML elements. These components can be used in web applications without the need for any additional frameworks or libraries.

## Server Side Rendering:
  
Server Side Rendering (SSR) is a technique used in web development where the server generates the initial HTML for a web page and sends it to the client's browser, which then renders the page. This is in contrast to Client Side Rendering (CSR), where the initial HTML is minimal and the bulk of the page rendering is done by JavaScript in the client's browser.

 
## Puppeteer:

Puppeteer is a Node.js library which provides a high-level API to control Chrome/Chromium over the DevTools Protocol. Puppeteer runs in headless mode by default, but can be configured to run in full ("headful") Chrome/Chromium.

  
## Express JS:
 
Fast, unopinionated, minimalist web framework for Node.js  
  

## Sample Web component

    <!DOCTYPE html>    
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Web Components | SSR (Server side rendering, doesn't need Javascript)</title>
    </head>
    <body>
    <custom-paragraph text="Custom Paragraph"></custom-paragraph>
    </body>
    <script>
    class CustomParagraph extends HTMLElement {
    constructor() {
    super();
    const text = this.getAttribute('text');
    this.innerHTML = `
    <template shadowrootmode="open">
    <style>
    p{
    font-size: 65px;
    font-weight: 400;
    font-style: italic;
    background-image: linear-gradient(to left, #007f4c, #53e3a7);
    color: black ;
    }
    </style>
    <p><slot></slot></p>
    </template>
    ${text}
    `;
    }
    }
    customElements.define("custom-paragraph", CustomParagraph);
    </script>
    </html>
    
[https://github.com/pradeepin2/web-components-server-side-rendering/blob/main/ssr.html](https://github.com/pradeepin2/web-components-server-side-rendering/blob/main/ssr.html)
  
  
  

## Rendering Webcomponent in Server before serving the request using Pupetter:


    const express = require("express");
    const fs = require('fs');
    const puppeteer = require("puppeteer");
    const app = express();
    const port = 4000;
    const content = fs.readFileSync("./ssr.html","utf-8").toString();
    app.get("/ssr", async(req,res) => {
	    const browser = await puppeteer.launch();
	    const page = await browser.newPage();
	    await page.setContent(content, {
				waitUntil: ["domcontentloaded"],
		});
	    const fullHTML = await page.content();
	    res.send(fullHTML);
    });
    app.listen(port, ()=>{
	    console.log(`Example Server side app running on: ${port}`);
    });


[https://github.com/pradeepin2/web-components-server-side-rendering/blob/main/ssr.js](https://github.com/pradeepin2/web-components-server-side-rendering/blob/main/ssr.js)


### Code Reference:
[https://github.com/pradeepin2/web-components-server-side-rendering/tree/main](https://github.com/pradeepin2/web-components-server-side-rendering/tree/main)

  
  
This technique can be applied on any web component, This is made possible with "Declarative Shadow DOM" Please checkout more details about Declarative Shadow DOM in my next post.
