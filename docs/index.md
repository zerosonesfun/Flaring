## ARCHIVED
This project is no longer active. Feel free to browse the code though. 🤓

![](https://i.ibb.co/WsYCvKG/428-E52-CF-7130-422-A-93-E6-334-B8-C21-A5-F2.png)

### Introduction
[Webrings](https://en.wikipedia.org/wiki/Webring) were cool in the 90s and it’s things like webrings that helped small websites out a lot. Now, everyone relies too much on promoting their projects via social media. But, social media is over crowded. A webring connects like websites together, promoting each other, in a simple way.

**Flaring** is a webring for webmasters who use the forum software Flarum. You just submit a few details about your site, copy and paste some code into your Flarum's custom footer, and now you are connected with other passionate Flarum communities. Here are the full rules and steps:

### How do I join?
This project is no longer active and so you cannot join.

### Widget code:
##### All you need to change is the url in line 1 which says "www.CHANGE_THIS_TO_YOUR_SITE.com," but please leave the ending slash and UTM code.
~~~
<webring-flaring site="https://www.CHANGE_THIS_TO_YOUR_SITE.com/?utm_source=flaring-surfer">
</webring-flaring>
<script>
const DATA_FOR_WEBRING = `https://raw.githubusercontent.com/zerosonesfun/Flaring/main/webring.json`;
const template = document.createElement("template");
template.innerHTML = `
<style>
#flaring-details {
  padding: 1rem; 
  text-align: left;
  font: 100% system-ui, sans-serif;
  cursor: pointer;
  color: #555;
}
#flaring-details a {
  color: #555;
}
</style>
<details id="flaring-details">
<summary>Explore</summary>
<div id="webring">
  <div id="webring-nav">
  </div>
</div></details>`;
class WebRing extends HTMLElement {
  connectedCallback() {
    this.attachShadow({ mode: "open" });
this.shadowRoot.appendChild(template.content.cloneNode(true));
    const thisSite = this.getAttribute("site");
    fetch(DATA_FOR_WEBRING)
      .then((response) => response.json())
      .then((sites) => {
        const matchedSiteIndex = sites.findIndex(
          (site) => site.url === thisSite
        );
        const matchedSite = sites[matchedSiteIndex];
        let prevSiteIndex = matchedSiteIndex - 1;
        if (prevSiteIndex === -1) prevSiteIndex = sites.length - 1;
        let nextSiteIndex = matchedSiteIndex + 1;
        if (nextSiteIndex > sites.length) nextSiteIndex = 0;
        const randomSiteIndex = this.getRandomInt(0, sites.length - 1);
        const cp = `
          <p>
            <a href="${matchedSite.url}">${matchedSite.name}</a> is a member of <a href="https://zerosonesfun.github.io/Flaring/" title="Learn More...">Flaring</a>.
          </p>
          <p>
            <a href="${sites[prevSiteIndex].url}">[Prev]</a>
            <a href="${sites[nextSiteIndex].url}">[Next]</a>
            <a href="${sites[randomSiteIndex].url}">[Random]</a>
          </p>
        `;
        this.shadowRoot
          .querySelector("#webring-nav")
          .insertAdjacentHTML("afterbegin", cp);
      });
  }
  getRandomInt(min, max) {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min + 1)) + min;
  }
}
window.customElements.define("webring-flaring", WebRing);

if(window.location.href.indexOf("flaring-surfer") > -1) {
       alert("Thanks for exploring and supporting the small communities within the Flaring webring. Look for an \"Explore\" link on this site when you're ready to check out the next community.");
} 
</script>
~~~

#### Welcome back to the 90s.
