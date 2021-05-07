<template>
  <div>
    <header class="header">
      <v-row justify="center">
        <h1 class="heading h2">HOW IT WORKS</h1>
      </v-row>
    </header>
    <section class="section">
      <v-row justify="center">
        <v-col>
          <h2>Simple upload form</h2>
          <p>
            We provide a simple upload form in order to use our free service.
            Just fill your email, select your data folders* and you are ready.
            We support data from Apple, Garmin, Fitbit, Huawei, Samsung and
            Xiaomi.<br />
            <i>*Each data folder must match to a seperated brand.</i>
          </p>
        </v-col>
        <v-col offset="1">
          <picture>
            <source
              srcset="/how-it-works/img1.jpg"
              media="(min-width: 1200px)"
            />
            <v-img
              src="/how-it-works/img1.jpg"
              alt="img1"
              max-width="500"
            ></v-img>
          </picture>
        </v-col>
      </v-row>
    </section>
    <section class="section">
      <v-row justify="center">
        <v-col>
          <picture>
            <source
              srcset="/how-it-works/img1.jpg"
              media="(min-width: 1200px)"
            />
            <v-img
              src="/how-it-works/img1.jpg"
              alt="img1"
              max-width="500"
            ></v-img>
          </picture>
        </v-col>
        <v-col offset="1">
          <h2>Security</h2>
          <p>
            Your data is safe. We delete your uploaded data after the completion
            of transformation. Your transformed data will be delete from our
            database in 7 days. We do not use any personal information that
            exist in the uploaded data.
          </p>
        </v-col>
      </v-row>
    </section>
    <section class="section">
      <v-row justify="center">
        <v-col>
          <h2>Transformation</h2>
          <p>
            We transform your data with the open source schema
            <a href="https://www.openmhealth.org/">Open mHealth</a>. So, you
            will not need to examine each wearable brand separated.
          </p>
        </v-col>
        <v-col offset="1">
          <picture>
            <source
              srcset="/how-it-works/img1.jpg"
              media="(min-width: 1200px)"
            />
            <v-img
              src="/how-it-works/img1.jpg"
              alt="img1"
              max-width="500"
            ></v-img>
          </picture>
        </v-col>
      </v-row>
    </section>
    <section class="section">
      <v-row justify="center">
        <v-col>
          <picture>
            <source
              srcset="/how-it-works/img1.jpg"
              media="(min-width: 1200px)"
            />
            <v-img
              src="/how-it-works/img1.jpg"
              alt="img1"
              max-width="500"
            ></v-img>
          </picture>
        </v-col>
        <v-col offset="1">
          <h2>Data export</h2>
          <p>
            After the data transformation you will recieve an email from us with
            the download link to download your merged data. We provode seperated
            csv files for each data category for simple import into your
            favorite stats software.
          </p>
        </v-col>
      </v-row>
    </section>
    <section class="section">
      <v-row justify="center">
        <v-col>
          <h2>Report pages (Comming soon)</h2>
          <p>
            Do you want to get live stats in yor data but you do not want to get
            mess with other softwares? Our report pages offer you a variety of
            ways to view different data types.
          </p>
        </v-col>
        <v-col offset="1">
          <picture>
            <source
              srcset="/how-it-works/img1.jpg"
              media="(min-width: 1200px)"
            />
            <v-img
              src="/how-it-works/img1.jpg"
              alt="img1"
              max-width="500"
            ></v-img>
          </picture>
        </v-col>
      </v-row>
    </section>
  </div>
</template>

<style>
.header {
  padding-top: 10px;
}
.section {
  padding-top: 92px;
  padding-bottom: 92px;
}
</style>
