<template>
  <div class>
    <footer id="footer" class="shadow pt-5">
      <div class="footer-top">
        <div class="container">
          <div class="row col-md-6 mx-auto">
            <div class="col-lg-9">
              <ul class="list-group list-unstyled">
                <li><a href="#">Home</a></li>
                <li><a href="#">About Us</a></li>
                <li><a href="#">Privacy Policy</a></li>
                <li><a href="#">Contact Us</a></li>
                <li><a href="#">Blog</a></li>
              </ul>
            </div>
            <div class="col-lg-3">
              <ul class="list-group list-unstyled">
                <li class="nav-item dropdown show">
                  <b>Language</b>
                  <b-dropdown
                    size="sm"
                    variant="outline"
                    text="English"
                    class="m-2"
                  >
                    <b-dropdown-item-button>English</b-dropdown-item-button>
                    <b-dropdown-item-button>French</b-dropdown-item-button>
                  </b-dropdown>
                </li>
                <li class="nav-item dropdown show">
                  <b>Country</b>
                  <b-dropdown
                    size="sm"
                    variant="outline"
                    text="Cameroon"
                    class="ml-2"
                  >
                    <b-dropdown-item-button>Cameroon</b-dropdown-item-button>
                    <b-dropdown-item-button>Nageria</b-dropdown-item-button>
                  </b-dropdown>
                </li>
              </ul>
            </div>
          </div>
        </div>
        <div class="mt-5 border-top">
          <div class="col-lg-12 mt-3">
            <p class="text-center">© Copyright all rights reserved</p>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
li {
  text-align: start;
  list-style: none;
}
.bottom {
  border-top: solid 1px #ccc;
  padding: 10px;
  text-align: center;
}
.top {
  padding: 50px;
  position: relative;
  left: 230px;
}

.pages {
  color: black;
  text-decoration: none;
}
.pages:hover {
  color: #e75c18;
}
.link {
  color: #e75c18;
  text-decoration: none;
}
@media only screen and (max-width: 768px) {
  .top {
    padding: 50px;
    position: relative;
    left: -40px;
  }

  .card {
    width: 500px;
  }
  .row {
    display: flex;
    flex-direction: column;
  }
  .bottom {
    margin-left: -150px;
  }
}
</style>

<style>
.nav-pills .nav-link.active,
.nav-pills .show > .nav-link {
  background-color: #e6e6e6;
}

</style>


<style >



::-webkit-scrollbar-track
{
	-webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
	background-color: #F5F5F5;
}

::-webkit-scrollbar
{
	width: 5px !important;
	background-color: #F5F5F5;
}

::-webkit-scrollbar-thumb
{
	background-color: #000000;
	border: 2px solid #555555;
}

  
</style>