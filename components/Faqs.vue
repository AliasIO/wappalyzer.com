<template>
  <div>
    <v-expansion-panels v-if="topic === 'lists'" flat>
      <v-expansion-panel>
        <v-expansion-panel-header>
          What are lead lists?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Our <nuxt-link to="/lists/">lead lists</nuxt-link> are lists of
            websites that use a certain
            <nuxt-link to="/technologies/">web technologies</nuxt-link>, along
            with email addresses and phone numbers. Lead lists help sales and
            marketing teams with prospecting, market research and competitor
            analysis.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          What information is included in the lists?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Lead lists include hostnames, version numbers, website country and
            language, traffic rank and metadata such as page title and
            description.
          </p>

          <p>
            On a
            <v-chip to="/pro/" color="primary" x-small outlined> PRO </v-chip>
            plan, available company and contact information such as employee
            counts, email addresses and phone numbers are included too.
          </p>

          <p>
            See the full list of
            <nuxt-link to="/docs/fields/">fields</nuxt-link>, all
            <nuxt-link to="/pro/">
              <v-chip to="/pro/" color="accent" x-small outlined>PRO</v-chip>
              features</nuxt-link
            >
            and a <nuxt-link to="/lists/sample/">lead list sample</nuxt-link>.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          What segmentation options are available?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Lead lists can be filtered by keyword, company industry and size,
            website traffic, IP country, top-level domain and language.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          A technology I'm looking for is not in the list, can it be added?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            You can
            <nuxt-link to="/technologies/suggest/"
              >suggest a new technology</nuxt-link
            >. We only accept web technologies with an established user base.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          What is IP country?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            IP country is the country a website's IP address belongs to.
            Typically this is where the website is hosted, which can be
            indicative of the location the business that owns the website
            operates from.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          How is the information being collected?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            We collect limited information through our
            <nuxt-link to="/apps/">browser extension</nuxt-link>
            in accordance with our
            <nuxt-link to="/privacy/">privacy policy</nuxt-link> and perform
            in-depth analysis using in-house crawlers. Our unique methods ensure
            only actively visited websites are included in the lists, including
            pages that traditional crawlers can't reach.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          How accurate is the data?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Out technology data is of a very high standard and corroborated
            across multiple sources. Email addresses and phone numbers obtain
            from websites' contact pages are unverified and as-is.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          How fresh is the data?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            The data is being updated and added to every day. By default, data
            in the lead lists can be up to three months old but this can be
            lowered down to one month.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          How do you determine website traffic?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Website traffic is tracked using our
            <nuxt-link to="/apps/">browser extensions</nuxt-link> with 1.5M
            users. The install base provides a large enough sample set to
            determine which websites receive more traffic than others, resulting
            in a relative traffic indicator.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          Can I use a different payment method?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Please <nuxt-link to="/contact/">contact us</nuxt-link> if you wish
            to pay via bank transfer or Bitcoin, or discuss options.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          Can I resell the data?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            No, not without explicit permission in writing. Please refer to the
            <nuxt-link to="/terms/">terms of use</nuxt-link> and
            <nuxt-link to="/contact/">contact us</nuxt-link> to discuss options.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          What is your refund policy?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            If you're not satisfied with the quality of a list for any reason,
            we'll work with you to resolve the problem or issue a refund. Please
            refer to the <nuxt-link to="/terms/">terms of use</nuxt-link>.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>

    <v-expansion-panels v-if="topic === 'api'" flat>
      <v-expansion-panel>
        <v-expansion-panel-header>
          What information is included in API responses?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            The APIs return hostnames, version numbers, website country and
            language, traffic rank and metadata such as page title and
            description.
          </p>

          <p>
            On a
            <v-chip to="/pro/" color="primary" x-small outlined> PRO </v-chip>
            plan, available company and contact information such as employee
            counts, email addresses and phone numbers are included too.
          </p>

          <p>
            See the full list of
            <nuxt-link to="/docs/fields/">fields</nuxt-link>.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          Where do I find my API key?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            You can create your API in the
            <nuxt-link to="/apikey/">API key</nuxt-link> tab in your account.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          How is the information being collected?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            We collect limited information through our
            <nuxt-link to="/apps/">browser extension</nuxt-link>
            in accordance with our
            <nuxt-link to="/privacy/">privacy policy</nuxt-link> and perform
            in-depth analysis using in-house crawlers. Our unique methods ensure
            only actively visited websites are included in the lists, including
            pages that traditional crawlers can't reach.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          How fresh is the data?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            The data is being updated and added to every day. By default, lookup
            results can be up to three months old but this can be lowered down
            to one month. Live results are real-time.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          How do you determine website traffic?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Website traffic is tracked using our
            <nuxt-link to="/apps/">browser extensions</nuxt-link> with 1.5M
            users. The install base provides a large enough sample set to
            determine which websites receive more traffic than others, resulting
            in a relative traffic indicator.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          Can I resell the data?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            No, not without explicit permission in writing. Please refer to the
            <nuxt-link to="/terms/">terms of use</nuxt-link> and
            <nuxt-link to="/contact/">contact us</nuxt-link> to discuss options.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          Do you offer a free trial?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Sign up for <nuxt-link to="/pricing/">free plan</nuxt-link> to get
            50 credits every month to use with the APIs and other products.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>

    <v-expansion-panels v-if="topic === 'pricing'" flat>
      <v-expansion-panel>
        <v-expansion-panel-header>
          Do I need to sign up for a plan?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            We accept one-time payments for lead lists, technology lookups and
            credits. A paid plan is required to access company and contact
            details and is usually more cost-effective, especially when making
            regular or higher volume purchases.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          <span>
            What are
            <span class="body-2">
              <v-chip color="primary" x-small outlined>PRO</v-chip></span
            >
            features?
          </span>
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            <v-chip to="/pro/" color="primary" x-small outlined> PRO </v-chip>
            features include CRM integrations and access to company and contact
            information in all of our data products, including lead lists,
            technology lookups, APIs and browser extension.
            <nuxt-link to="/pro/">
              See all
              <v-chip to="/pro/" color="accent" x-small outlined> PRO </v-chip>
              features</nuxt-link
            >.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          Can I cancel my plan any time?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Yes, you can cancel your plan any time without losing access to your
            credits or past purchases.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header> What are credits? </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Credits can be spent on a range of products, including lead lists
            and APIs. Each product has a fixed spend per unit, detailed on the
            <nuxt-link :to="{ path: '/pricing/', hash: '#usage' }"
              >pricing</nuxt-link
            >
            page.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          When do credits expire?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Credits included in plans expire after 60 days. Credits purchased
            directly expire after 365 days. Expired credits can no longer be
            used.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          Can I use a different payment method?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Plans can only be purchased with a credit card. Credits and other
            products can be purchased directly using a credit card or PayPal
            account. Please
            <nuxt-link to="/contact/">contact us</nuxt-link> if you wish to pay
            via bank transfer or Bitcoin, or discuss options.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          What is your refund policy?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            If you're dissatisfied with the quality of our offering we will
            either work with you to resolve the issue, credit your account or
            issue a pro-rata refund. Credits are generally non-refundable.
            Please refer to the
            <nuxt-link to="/terms/">terms of use</nuxt-link>.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>

    <v-expansion-panels v-if="topic === 'extension'" flat>
      <v-expansion-panel>
        <v-expansion-panel-header>
          What's the 'more info' tab about?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          The browser extension shows the technologies a websites uses, for
          free. On a
          <v-chip to="/pricing/" color="primary" x-small outlined> PRO </v-chip>
          plan, the 'more info' tab reveals available company and contact
          information for the website as well as social media profiles and any
          other metadata we find.
          <nuxt-link to="/pro/"
            >See all
            <v-chip to="/pro/" color="accent" x-small outlined> PRO </v-chip>
            features</nuxt-link
          >.

          <v-card class="my-8" :max-width="1118 * 0.5">
            <v-img
              src="/images/faqs/extension-pro.png"
              alt="Wappalyzer PRO extension"
            />
          </v-card>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          Can I suggest a technology to be added?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            The browser extension is open-source. If you are a developer or have
            access to one, please refer to our
            <a
              href="https://github.com/AliasIO/wappalyzer/blob/master/CONTRIBUTING.md"
              rel="noopener"
              target="_blank"
              >contributing guide</a
            >. Otherwise, please
            <a
              href="https://github.com/AliasIO/wappalyzer/issues/new/choose"
              rel="noopener"
              target="_blank"
              >create an issue</a
            >
            on GitHub.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          Where can I report a bug or request a new feature?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Please
            <a
              href="https://github.com/AliasIO/wappalyzer/issues/new/choose"
              rel="noopener"
              target="_blank"
              >create an issue</a
            >
            on GitHub.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          How does the extension work?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            The extension inspects HTML, scripts, cookies and network requests
            and certificates of pages you visit, looking for unique technology
            fingerprints.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          Can I hide technologies on my website from Wappalyzer?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            Although in many cases it's possible to change a software
            application's output to obfuscate its charactaristics, it's often
            impractical and unnecessary. If you're worried about security,
            ensure your software is always up-to-date. For more information, see
            <nuxt-link to="/articles/how-to-hide-technologies-from-wappalyzer/"
              >How to hide technologies from Wappalyzer</nuxt-link
            >.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>

      <v-expansion-panel>
        <v-expansion-panel-header>
          What information do you collect?
        </v-expansion-panel-header>
        <v-expansion-panel-content eager>
          <p>
            We collect information in accordance with our
            <nuxt-link to="/privacy/">privacy policy</nuxt-link>. By default,
            when you visit a website, we record the domain name and identified
            technologies in a way that can't be traced back to you. You can
            disable this behaviour in the extension's settings.
          </p>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
  </div>
</template>

<script>
export default {
  props: {
    topic: {
      type: String,
      default: 'lists',
    },
  },
}
</script>
