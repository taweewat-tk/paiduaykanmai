<template>
  <div class="d-flex justify-content-between p-4">
    <div class="logo">
      Front-End Developer
    </div>

    <div class="d-flex justify-content-center">
      <b-nav pills align="center">
        <b-nav-item to="/" exact exact-active-class="active">
          Home
        </b-nav-item>
        <b-nav-item to="/pokemon" exact exact-active-class="active">
          Pokemon
        </b-nav-item>
        <b-nav-item to="/function1" exact exact-active-class="active">
          Function 1
        </b-nav-item>
        <b-nav-item to="/function2" exact exact-active-class="active">
          Function 2
        </b-nav-item>
        <b-nav-item to="/function3" exact exact-active-class="active">
          Function 3
        </b-nav-item>
      </b-nav>
    </div>
  </div>
</template>

<style>
  .logo{
    font-size: 27px;
    font-weight: bold;
    background-image: linear-gradient(-90deg, #65c6af, #4daaa3, #3e8e93, #37737f, #325967);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .active{
    color: #3e8e93 !important;
    background-color: #fff !important;
    font-weight: bold;
  }
  .nav-link{
    color:#454545;
  }
  .nav-link:hover{
    color: #3e8e93 !important;
    background-color: #fff !important;
  }
</style>
