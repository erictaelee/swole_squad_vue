         <template>
         <!-- Team-->
        <section class="page-section bg-light" id="team">
            <div class="container">
                <div class="text-center">
                    <br />
                    <h2>Welcome Arnold!</h2>
                    <br />
                    <h2 class="section-heading text-uppercase">Select Your Trainer</h2>
                    <!-- <h3 class="section-subheading text-muted">Lorem ipsum dolor sit amet consectetur.</h3> -->
                </div>
                <div class="row">
                    <div class="col-lg-4">
                        <div class="team-member">
                            <a href="/muscles"><img class="mx-auto rounded-circle" src="assets/img/team/eric3.jpg"  alt="..." /></a>
                            <h4>Eric Lee</h4>
                            <p class="text-muted">Chicago, IL</p>
                            <p class="text-muted">Men's Physique Competitor</p>
                            <a class="btn btn-dark btn-social mx-2" href="#!"><i class="fab fa-twitter"></i></a>
                            <a class="btn btn-dark btn-social mx-2" href="#!"><i class="fab fa-facebook-f"></i></a>
                            <a class="btn btn-dark btn-social mx-2" href="#!"><i class="fab fa-linkedin-in"></i></a>
                        </div>
                    </div>
                    <div class="col-lg-4">
                        <div class="team-member">
                            <a href="#"><img class="mx-auto rounded-circle" src="assets/img/team/rolando.jpg" alt="..." /></a>
                            <h4>Coming Soon..</h4>
                            <p class="text-muted">Rockford, IL</p>
                            <p class="text-muted">Pro Men's Body Building Competitor</p>
                            <a class="btn btn-dark btn-social mx-2" href="#!"><i class="fab fa-twitter"></i></a>
                            <a class="btn btn-dark btn-social mx-2" href="#!"><i class="fab fa-facebook-f"></i></a>
                            <a class="btn btn-dark btn-social mx-2" href="#!"><i class="fab fa-linkedin-in"></i></a>
                      
                        </div>
                    </div>
                    <div class="col-lg-4">
                        <div class="team-member">
                            <a href="#"><img class="mx-auto rounded-circle" src="assets/img/team/fritz2.jpg" alt="..." /></a>
                            <h4>Coming Soon..</h4>
                            <p class="text-muted">San Francisco, CA</p>
                            <p class="text-muted">Pro Men's Physique Competitor</p>
                            <a class="btn btn-dark btn-social mx-2" href="#!"><i class="fab fa-twitter"></i></a>
                            <a class="btn btn-dark btn-social mx-2" href="#!"><i class="fab fa-facebook-f"></i></a>
                            <a class="btn btn-dark btn-social mx-2" href="#!"><i class="fab fa-linkedin-in"></i></a>
                        </div>
                    </div>
                </div>
                <!-- <div class="row">
                    <div class="col-lg-8 mx-auto text-center"><p class="large text-muted">Do you want to know what exercises they do to get to where they are? Click the trainer and find out how they workout their muscles. </p></div>
                </div> -->
            </div>
        </section>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      name: "",
    };
  },

  created: function () {},
  methods: {
    showName: function () {
      return localStorage.getItem("name");
    },
  },
};
</script>
