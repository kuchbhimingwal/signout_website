<template>
    <div class="footer-copyright">
      <div class="row foot">
        <div class="col s2 copyright"><a href="https://durhamcollege.ca/programs-and-courses">© Durham College 2010 - 2020</a></div>
        <div class="col s2 push-s8 link"><a href="https://durhamcollege.ca/mycampus/">Durham College | MyCampus</a></div>
      </div>
    </div>
</template>

<script>
export default {
    name: 'Footer',
    components: {
    
    }
}
</script>
<style>
.foot{
    margin-bottom: 0;
    background-color: #008265;
    height: 3.0rem;
}
.copyright a, .link a{
    color: black;
    line-height: 3.0rem;
}
.copyright, .link{
    font-size: 13px;
    line-height: 2.0rem;
}
</style>