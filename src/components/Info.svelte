<script>
  import ExamplePlot from './ExamplePlot.svelte'
</script>

<style>

</style>

<div class="bg-light py-3" id="info">
  <div class="container">
    <!-- <h4 class="text-center display-4 mb-4">What is all of this?</h4> -->
    <div class="row">
      <!-- <div class="col-md-6">
        <h3 class="text-center">A Simplified Seir Model</h3>
        <p class="text-justified font-weight-bold">What is a seir model?</p>
        <p class="text-justified">
          A seir model is a complex model used by epidimiologists. It breaks people into
          different based on their state of having the disease. Because those models can
          be quite confusing and hard to understand, we have tried to take the important
          info from our model to show to you.
        </p>
        <p class="text-justified font-weight-bold">Where is the data coming from?</p>
        <p class="text-justified">
          The data is being derived from
          <a href="http://yetanotherseirmodel.com/" target="_blank">this seir model</a>
          using data from what has already happened to predict how the outbreaks will
          continue in the future. If you want to derive the data yourself you can using
          the complex model, but we've done all the hard work for you already so you don't
          have to.
        </p>
        <p class="text-justified font-weight-bold">What is R&#8320;?</p>
        <p class="text-justified">
          R&#8320; is a number used by many epidemiologists that goes along with a seir
          model. R&#8320; describes, on average, how many people one sick person will pass
          the virus to. This is extremely important because when R&#8320; is greater than
          1, then the virus will spread, but if it is less than 1 then it will not.
        </p>
        <p class="text-justified font-weight-bold">
          What is the effective R&#8320; (R&#8337;)?
        </p>
        <p class="text-justified">
          Our model is centered around this R&#8337; value. This value is found by simply
          multiplying the percent of the population susceptible to the disease by the
          R&#8320; value. This tells us how much the disease is actually spreading.
        </p>
      </div>
      <div class="col-md-6">
        <h3 class="text-center">All About Herd Immunity</h3>
        <details>
          <summary class="text-justified font-weight-bold">
            What is herd immunity?
          </summary>
          <p>
            Herd immunity is a term used to describe a community in which enough people
            have been infected such that the number of new cases of the virus can no
            longer increase because enough people are immune. Herd immunity can be
            acheived through a vaccine or enough people having the antibodies.
          </p>
        </details>
        <p class="text-justified font-weight-bold">What is herd immunity?</p>
        <p class="text-justified">
          Herd immunity is a term used to describe a community in which enough people have
          been infected such that the number of new cases of the virus can no longer
          increase because enough people are immune. Herd immunity can be acheived through
          a vaccine or enough people having the antibodies.
        </p>
        <p class="text-justified font-weight-bold">
          How do we know when we reached herd immunity?
        </p>
        <p class="text-justified">
          Well this is a complicated question! There is no single threshold that means
          herd immunity has been reached. This varies place to place from as small scale
          as towns to as big as countries. Using the data from the beginning of the
          pandemic we try to predict what percentage of the population must be immune for
          a state to reach herd immunity based on how fast the virus initially spread.
        </p>
        <p class="text-justified font-weight-bold">
          So when there's not a lot of cases herd immunity has been reached?
        </p>
        <p class="text-justified">
          Not exactly. Most places around the world right now are not operating at 100%
          right now. This means the number of interactions that are happening are less
          than during the "normal time" so the virus spreads slower. This is good because
          we are able to limit the number of cases, but does not mean we can simply return
          to normal immediately.
        </p>
        <p class="text-justified font-weight-bold">
          But when we do reach herd immunity there won't be anymore cases right?
        </p>
        <p class="text-justified">
          Again this is not exactly true. Even when herd immunity has been reached people
          who are not immune can still contract the disease, but the disease likely will
          not have another ouotbreak where cases grow rapidly and out of control.
        </p>
      </div>
      <hr class="col-12" />-->
      <div class="col-12">
        <h2 class="text-center display-4 mb-4">How to interpret this graphic</h2>
      </div>
      <div class="col-md-5 col-lg-4">
        <img src="img/R0_params.png" alt="Example plot" class="img-fluid" />
      </div>
      <div class="col-md-7 col-lg-8">
        <!-- <p class="text-justified">
          To understand our herd immunity status, we have to think in terms of R&#8320;,
          which is a measure of how many people each infected person passes the virus on
          to. If R&#8320; were exactly 1, then the epidemic would neither grow or shrink,
          since each infected person infect one other person before they were no longer
          infectious. R&#8320; &gt; 1 leads to an exponentially rising number of cases,
          and below 1, the epidemic will fade away. But if some fraction of the people
          that get exposed to the virus are no longer susceptible, the actual number of
          new infections will be reduced from the full R&#8320;. For example, if 50% of
          the population is susceptible then only half of the number of exposures implied
          by R&#8320; will lead to new infections. If few enough people are still
          susceptible to bring these actual new infections to 1 or less, we have achieved
          herd immunity. So, if we can estimate R&#8320; and the remaining population
          susceptible, then we can determine our herd immunity status. Sounds simple… but
          it’s not! We need to predict these parameters from the testing and data we
          collect.
        </p> -->
        <p class="text-justified">
          The number of people we pass a virus to (R&#8320;) is directly related to the
          amount of interaction we have with others. At the beginning of the epidemic, our
          society was in its natural highly interactive “old normal” state (shown in green
          in the figure), and R&#8320; was high. In response to the danger and uncertainty
          of the virus, we drastically lowered our level of interaction, and R&#8320;
          became far lower (red region), We then began to relax restrictions and settled
          into a “new normal R&#8320;”, and eventually, we hope to return to our “old
          normal” levels. Similarly, as the virus progresses, the number of susceptible
          people remaining, which started at 100%, is gradually being reduced. Using
          standard epidemiological models coupled with the case and fatality data for a
          given location, we can estimate these R&#8320; levels and timing of the
          transitions, as well as how many susceptible people remain.
        </p>
        <p class="text-justified">
          Our graphic below shows you the results of this work.
        </p>
      </div>
    </div>
    <!-- <hr />
    <ExamplePlot /> -->
  </div>
</div>
