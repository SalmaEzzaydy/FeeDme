<template>
  <footer>
    <div class="container pt-5">
      <div class="row">
        <div class="col-md-3 col-6">
          <ul style="list-style-type: none">
            <li class="text-light font-weight-bold pb-2">Get to Know Us</li>
            <li><a class="footer-link font-weight-light" href="#">About Us</a></li>
            <li><a class="footer-link font-weight-light" href="#">Our meals</a><br></li>
            <li><a class="footer-link font-weight-light" href="#">Our top categories</a><br></li>
          </ul>
        </div>

        <div class="col-md-3 col-6">
          <ul style="list-style-type: none">
            <li class="text-light font-weight-bold">Connect With Us</li>
            <li><a class="footer-link font-weight-light" href="#">Facebook</a></li>
            <li><a class="footer-link font-weight-light" href="#">Twitter</a><br></li>
            <li><a class="footer-link font-weight-light" href="#">Instagram</a><br></li>
          </ul>
        </div>

        <div class="col-md-3 col-6">
          <ul style="list-style-type: none">
            <li class="text-light font-weight-bold">Enjoy meals with Us</li>
            <li><a class="footer-link font-weight-light" href="#">Different countries meals</a></li>
            <li><a class="footer-link font-weight-light" href="#">Delicious meals</a><br></li>
            <li><a class="footer-link font-weight-light" href="#">100% healthy</a><br></li>
          </ul>
        </div>

        <div class="col-md-3 col-6">
          <ul style="list-style-type: none">
            <li class="text-light font-weight-bold">Let Us Help You</li>
            <li><a class="footer-link font-weight-light" href="#">Return Centre</a></li>
            <li><a class="footer-link font-weight-light" href="#">100% Purchase Protection</a><br></li>
            <li><a class="footer-link font-weight-light" href="#">Help</a><br></li>
            <li><a class="footer-link font-weight-light" href="#">App Download</a><br></li>
          </ul>
        </div>
      </div>

      <div class="row">
        <div class="col-12">
          <div class="text-center py-5">
            <router-link :to="{ name: 'Home' }">
              <img id="logo" src="../assets/icon0.png" />
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name : "Footer"
}
</script>

<style>
footer {
  margin-top : 100px;
  background-color:#232F3E;
  font-size:16px;
}

li {
  padding-left: 0;
  padding-bottom: 10px;
}

a {
  text-decoration: none;
}

.footer-link {
  color: #DDD;
}

#logo {
  width: 150px;
}


footer {
  font-family: 'Roboto', sans-serif;
}


</style>
