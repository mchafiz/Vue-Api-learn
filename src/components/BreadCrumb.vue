<template>
   <div class="row mt-4">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-dark">Foods</router-link>
              </li>

              <li class="breadcrumb-item active" aria-current="page">
                <router-link :to="$route.path" class="text-dark"
                  >{{title}}</router-link
                >
              </li>
            </ol>
          </nav>
        </div>
      </div>
</template>

<script>
export default {
  name: "breadcrumb",
  props:['title'],

};

</script>

