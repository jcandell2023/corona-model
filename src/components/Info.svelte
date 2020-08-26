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
      <hr class="col-12" /> -->
      <div class="col-12">
        <h2 class="text-center display-4 mb-4">How to interpret this graphic</h2>
      </div>
      <div class="col-md-5 col-lg-4 col-xl-3">
        <img src="img/R0_params.png" alt="Example plot" class="img-fluid" />
      </div>
      <div class="col-md-7 col-lg-8 col-xl-9">
        <p class="text-justified">
          Our graph has 3 lines and 1 circle per state. Each line represents one of the
          values in this example plot and the circle represents the percent of the
          population still susceptible in the state. The green line represents the initial
          R&#8320; in the state, refered to as the "Old Normal R&#8320;". The red line
          represents the R&#8320; during the lockdown in the state, referred to as the
          "Crisis R&#8320;". Finally, the orange line represents the current R&#8320; in
          the state, refered to as the "New Normal R&#8320;" In our graph, the "old
          normal" and "crisis" R&#8320; are constant, and the "new normal" R&#8320; shows
          how a state is adjusting their guidelines with a higher R&#8320; meaning they
          are more open.
        </p>
      </div>
    </div>
    <!-- <hr />
    <ExamplePlot /> -->
  </div>
</div>
