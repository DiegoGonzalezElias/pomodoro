
<script setup>
import { Icon } from '@iconify/vue';
</script>

<template>
    <div class="sidebar">
        <div class="avatar">
          <img class="avatar-img" src="../assets/lizard-avatar.webp">
        <!-- Aquí puedes agregar la imagen o icono del avatar -->
        </div>
        <ul class="sidebar--iconsBetween">
            <div class="sidebar__topIcons">
                <li>
                    <RouterLink to="/">
                        <Icon icon="bxs:home" color="white" width="40" height="40" />
                    </RouterLink>
                </li>
                <li>
                    <RouterLink to="/about">
                        <Icon icon="ion:stats-chart" color="white" width="40" height="40" />
                    </RouterLink>
                </li>
    
     
            </div>

            
            <li>
                <RouterLink to="/logout">
                    <Icon icon="heroicons-outline:logout" color="white" width="40" height="40" />
                </RouterLink>
            </li>

        </ul>
  </div>
</template>


<style lang="scss" scoped>
.sidebar {
  width: 80px;
  min-height: 100VH;
  background-color: #4D61D2;
  padding: 0 20px;
  margin: 0;
  display: flex;
  flex-direction: column;
  align-items: center;

  .avatar {
    margin-top: 20px;
    width: 80px;
    height: 80px;
    border-radius: 50%;
    border: solid 2px white;
    background-color: #ccc;
    /* Estilos adicionales para el avatar */
  }

  .avatar-img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 50%;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 20px 0;

    li {
      padding: 20px;
      width: 100%;
      display: flex;
      justify-content: center;
      margin-bottom: 10px;

      a {
        text-decoration: none;
        color: white;
        font-family: "Montserrat Alternates";

        &:hover {
          color: #000;
        }
      }
      &:hover {
        background-color: #3d4da5; /* Cambia el color de fondo al hacer hover */
      }
    }
  }
}
.sidebar--iconsBetween{
    width: 100%;
    height: 80vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
}

.sidebar__topIcons{
    width: 100%;
    align-items: center;
    margin-top: 40px;
    display: flex;
    flex-direction: column;
    
}
</style>