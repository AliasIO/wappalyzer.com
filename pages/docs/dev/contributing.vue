<template>
  <div>
    <Page :title="title" :side="side" no-head>
      <h1 id="contributing" class="mb-4">
        Contributing
        <a href="#contributing">
          <v-icon color="accent">mdi-link</v-icon>
        </a>
      </h1>

      <p>
        Wappalyzer is
        <a
          href="https://github.com/aliasio/wappalyzer/blob/master/LICENSE"
          target="_blank"
          g
        >
          open-source </a
        >. Anyone who wishes to contribute is welcome to do so! Wappalyzer has
        been improved by
        <a
          href="https://github.com/aliasio/wappalyzer/graphs/contributors"
          target="_blank"
          g
          >hundreds of people</a
        >
        over the years.
      </p>

      <h2 id="getting-started" class="mt-8 mb-2">
        Getting started
        <a href="#getting-started">
          <v-icon color="accent">mdi-link</v-icon>
        </a>
      </h2>

      <p>
        To get started, install
        <a href="https://git-scm.com/" target="_blank" g>Git</a>
        and
        <a href="https://www.docker.com/" target="_blank" g>Docker</a>
        on your system. This will allow you to install and run the Wappalyzer
        development environment which comes bundled with the required tools.
      </p>

      <p>
        Next,
        <a
          href="https://help.github.com/articles/fork-a-repo/"
          target="_blank"
          g
          >create a fork</a
        >
        of the
        <a href="https://github.com/aliasio/wappalyzer" target="_blank" g
          >Wappalyzer repository</a
        >
        on GitHub, clone it and execute <code>./run links</code> in
        <a
          href="https://en.wikipedia.org/wiki/Bash_(Unix_shell)"
          target="_blank"
          g
          >Bash</a
        >.
      </p>

      <pre
        class="mb-4"
      ><Prism language="bash" class="body-2">$ git clone https://github.com/&lt;your_github_username&gt;/wappalyzer.git
$ cd wappalyzer
$ ./run links</Prism></pre>

      <h2 id="drivers" class="mt-8 mb-2">
        Drivers
        <a href="#drivers">
          <v-icon color="accent">mdi-link</v-icon>
        </a>
      </h2>

      <p>
        Wappalyzer is a cross-platform application, written in JavaScript.
        Platform specific code can be found in
        <a
          href="https://github.com/aliasio/wappalyzer/tree/master/src/drivers"
          target="_blank"
          g
          ><code>src/drivers</code></a
        >. Shared functionality is contained within
        <a
          href="https://github.com/aliasio/wappalyzer/blob/master/src/wappalyzer.js"
          target="_blank"
          g
          ><code>src/wappalyzer.js</code></a
        >.
      </p>

      <p>
        To test your local changes in a browser, refer to the links below. The
        extension files are located in
        <a
          href="https://github.com/aliasio/wappalyzer/tree/master/src/drivers/webextension"
          target="_blank"
          g
          ><code>src/drivers/webextension</code></a
        >.
      </p>

      <ul class="mb-4">
        <li>
          <a
            href="https://developer.chrome.com/extensions/getstarted#unpacked"
            target="_blank"
            g
            >Google Chrome: load an unpacked extension</a
          >
        </li>
        <li>
          <a
            href="https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Temporary_Installation_in_Firefox"
            target="_blank"
            g
            >Mozilla Firefox: load a temporary add-on</a
          >
        </li>
      </ul>

      <p>
        Installation and usage instructions for NPM and Docker can be found on
        the
        <nuxt-link to="/download">download page</nuxt-link>.
      </p>

      <h2 id="submitting-changes" class="mt-8 mb-2">
        Submitting changes
        <a href="#submitting-changes">
          <v-icon color="accent">mdi-link</v-icon>
        </a>
      </h2>

      <p>
        When you're done making changes, run <code>./run validate</code>. If no
        errors are reported, push your commits to a new branch on your own
        repository.
      </p>

      <p>
        Finally, open a
        <a
          href="https://help.github.com/articles/about-pull-requests/"
          target="_blank"
          >pull request</a
        >
        on the
        <a href="https://github.com/AliasIO/Wappalyzer/pulls" target="_blank" g
          >Wappalyzer repository</a
        >. If the automated checks or members of the community report any
        issues, please resolve them or your pull request may get rejected.
      </p>

      <h2 id="adding-a-new-application" class="mt-8 mb-2">
        Adding a new application
        <a href="#adding-a-new-application">
          <v-icon color="accent">mdi-link</v-icon>
        </a>
      </h2>

      <p>
        To add a new application, edit
        <a
          href="https://github.com/aliasio/wappalyzer/blob/master/src/apps.json"
          target="_blank"
          ><code>src/apps.json</code></a
        >
        and add a square icon to
        <a
          href="https://github.com/aliasio/wappalyzer/tree/master/src/icons"
          target="_blank"
          ><code>src/icons</code></a
        >
        (preferably an SVG file, otherwise a 64x64 or 32x32 PNG file).
      </p>

      <p>
        Only widely used applications should be added. When creating a pull
        request, please include ten or more links to websites that use the
        application, a GitHub page with at least 1,000 stars or anything that
        will help establish the size of the user base.
      </p>

      <p>
        Wappalyzer uses
        <a
          href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions"
          target="_blank"
          >regular expressions</a
        >
        to fingerprint web applications. Refer to the
        <a href="specification">specification</a> for more detail.
      </p>

      <h2 id="adding-a-new-category" class="mt-8 mb-2">
        Adding a new category
        <a href="#adding-a-new-category">
          <v-icon color="accent">mdi-link</v-icon>
        </a>
      </h2>

      <p>
        Please
        <a href="https://github.com/aliasio/wappalyzer/issues" target="_blank"
          >open an issue on GitHub</a
        >
        first to discuss the need for a new category. To add one, edit
        <code>src/apps.json</code> and update the
        <a
          href="https://github.com/aliasio/wappalyzer/tree/master/src/drivers/webextension/_locales"
          target="_blank"
          g
          >translations</a
        >
        (it's acceptable to include the English string in any or all of them).
      </p>

      <h2 id="adding-a-new-translation" class="mt-8 mb-2">
        Adding a new translation
        <a href="#adding-a-new-translation">
          <v-icon color="accent">mdi-link</v-icon>
        </a>
      </h2>

      <p>
        To add a new translation, copy the <code>en</code> folder in
        <a
          href="https://github.com/aliasio/wappalyzer/tree/master/src/drivers/webextension/_locales"
          target="_blank"
          ><code>src/drivers/webextension/_locales</code></a
        >, rename it to the relevant two-letter country code and update the
        containing <code>messages.json</code>.
      </p>

      <h2 id="adding-a-new-feature" class="mt-8 mb-2">
        Adding a new feature
        <a href="#adding-a-new-feature">
          <v-icon color="accent">mdi-link</v-icon>
        </a>
      </h2>

      <p>
        Please
        <a href="https://github.com/aliasio/wappalyzer/issues" target="_blank"
          >open an issue on GitHub</a
        >
        first. New features and large changes are rarely accepted without prior
        discussion.
      </p>
    </Page>
  </div>
</template>

<script>
import Page from '~/components/Page.vue'
import side from '~/assets/json/nav/docs.json'

export default {
  components: {
    Page
  },
  data() {
    return {
      title: 'Developer documentation',
      side
    }
  }
}
</script>
