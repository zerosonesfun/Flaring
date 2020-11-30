![](https://i.ibb.co/WsYCvKG/428-E52-CF-7130-422-A-93-E6-334-B8-C21-A5-F2.png)

## Flaring - A webring
[img]https://i.ibb.co/WsYCvKG/428-E52-CF-7130-422-A-93-E6-334-B8-C21-A5-F2.png[/img]

### Introduction
[Webrings](https://en.wikipedia.org/wiki/Webring) were cool in the 90s and it’s things like webrings that helped small websites out a lot. Now, everyone relies too much on promoting their projects via social media. But, social media is over crowded. A webring connects like websites together, promoting each other, in a simple way.

**Flaring** is a webring for webmasters who use the forum software Flarum. You just submit a few details about your site, copy and paste some code into your Flarum's custom footer, and now you are connected with other passionate Flarum communities. Here are the full rules and steps:

### How do I join?
1. Your website must have Flarum installed.
2. Your website's primary language must be English. Sorry in advance to the many non-English sites, but in order to approve your site all moderators have to be able to easily read it. Different webrings for different countries could be set up in the future.
3. Your website cannot be about anything illegal or contain porn.
4. Your website must be "independent" and/or relatively small. The moderators of Flaring determine if your site meets this criteria.
5. Submit your site's information. You may do this by adding to the [webring.json](https://github.com/zerosonesfun/Flaring/blob/main/webring.json) file and submitting a pull request if you are familiar with GitHub. Or, simply fill out the form at the bottom of this page.
6. In order to become a fully approved Flaring webring member, you will need to also copy and paste the following widget code into your Flarum’s custom footer (which can be done from the Appearance settings). Or, copy and paste it into a dedicated page as long as the link to that page is part of a main menu and the link text is "**Explore**." Why **Explore**? Because this gives the average web surfer something common to look for as they go from site to site. Not everyone can place the webring navigation in their footer, but if everyone at least uses "Explore," then it makes it a little easier for the surfer to spot it.

### Widget code:
##### All you need to change is the url in line 1 which says "www.CHANGE_THIS_TO_YOUR_SITE.com," but please leave the ending slash and UTM code.
~~~
<webring-flaring site="https://www.CHANGE_THIS_TO_YOUR_SITE.com/?utm=flaring-surfer">
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

P.S. A working example is at the bottom of https://www.wilcosky.com.
