---
title: "Coding a Youtube Athlete Clone"
date: 2020-03-17T22:06:30-04:00
draft: false
---

### Idea behind this project
Web App that host videos of student athletes and provides recruiters an easy way to find athletes. Think Youtube but for sports recruiting. 
This project has a bunch of new concepts I've never implemented so this should be interesting. 

## Stack 

| FrontEnd   | Backend |
|------------|------------|
| React      | Express    |
|            |            |

I prefer to build my personal projects one step at a time in two separate parts(frontend | backend). 
So I start building the full frontend, then my backend, then integrating them together.

I like building the front end first for two reasons.
* I am forced to make my app look the way I want instead of what is easiest for me to implement with my backend. Makes my projects a little more realistic.
* If I stop building after the frontend, I can always deploy that as a template front end. This is better than a half finished full stack project

So let's start! 
# Front End

{{< highlight bash "linenos=false" >}}
    mkdir suplex-video
    cd suplex-video
    npx create-react-app client
    cd client
    npm start
{{< / highlight >}}
*The frontend should now be running locally!*

Let's go through and remove all the stuff we don't need. 
I've listed the file hierarchy and the changes we're making

I found my sample videos from https://www.pexels.com/search/videos/sport. They're super high quality and free to download

```
suplex-video 
│
└───Client
    │   .gitignore
    │   .git
    |   package-lock.json
    |   package.json
    |   README.md
    │
    └───node_modules
    |   │   [This is where all your dependencies are. I'm not listing all 1024 base dependencies.]
    │
    └───public 
    |   │   favicon.ico [DELETE]
    |   │   index.html
    |   │   logo192.png [DELETE]
    |   │   logo512.png [DELETE]
    |   │   manifest.json
    |   │   robots.txt
    |   |
    |   └───Videos [CREATE]
    |       |   Sample.mp4 [CREATE]
    |       |   Sample2.mp4 [CREATE]
    |       |   Sample3.mp4 [CREATE]   
    |
    └───src
        │   App.css [DELETE ALL CONTENT]  {{< myshortcode spacing="      |   " shownText="App.js [UPDATE]" >}}
import React from 'react';
import './App.css';

function App() {
  return (
    <div className='App'>
    <h1> Base Frontend</h1>
    </div>
  );
}

export default App;
{{< /myshortcode >}}        |   App.test.js [DELETE]
        |   index.css
        |   logo.svg [DELETE]
        │   serviceWorker.js
        |   setupTests.js
        |   
        └───components [CREATE]
```

We now have our absolute base frontend. Let's start with displaying the videos. 

This is pretty simple but a little different in React w/ JSX. Go ahead and create a IndividualVideo.js file inside your components folder. 
Next is to render the videos from our public folder:


#### *IndividualVideo.js*
{{< highlight React "linenos=false" >}}
import React from "react"

const IndividualVideo = ({src}) => {

return (<div style={{width: "400px", padding: "2rem"}}>
      <video id="video1" height="500"  width= "400px" src={src} type="video/mp4" controls />
      <p> Description</p>
      <div style={{display: "flex", justifyContent: "center"}}>
        <div >Upvote</div>
        <div>Upvote</div>
        <div>Upvote</div>
      </div>
      </div>  
)}

export default IndividualVideo;
{{< / highlight >}}

We will of course need to import this into our App.js and I added a tiny bit of styling for future so it should look something like this: 


#### *App.js*
{{< highlight React "linenos=false" >}}
import React from 'react';
import './App.css';
import IndividualVideo from "./components/IndividualVideo.js"

function App() {
  return (
    <div className="App">
      <h1> Base Frontend </h1>
      <div style={{display: "flex", flexDirection: "column"}}>
        <IndividualVideo src="/videos/Sample.mp4"/>
        <IndividualVideo src="/videos/Sample2.mp4"/>
        <IndividualVideo src="/videos/Sample3.mp4"/>
      </div>
    </div>
  );
}

export default App;

{{< / highlight >}}
