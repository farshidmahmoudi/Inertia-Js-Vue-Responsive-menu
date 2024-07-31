<script setup>
import { ref } from 'vue';
import { Head, Link, router } from '@inertiajs/vue3';
import ApplicationMark from '@/Components/ApplicationMark.vue';
import Banner from '@/Components/Banner.vue';
import Dropdown from '@/Components/Dropdown.vue';
import DropdownLink from '@/Components/DropdownLink.vue';
import NavLink from '@/Components/NavLink.vue';
import ResponsiveNavLink from '@/Components/ResponsiveNavLink.vue';

defineProps({
    title: String,
});

const showingNavigationDropdown = ref(false);

const switchToTeam = (team) => {
    router.put(route('current-team.update'), {
        team_id: team.id,
    }, {
        preserveState: false,
    });
};

const logout = () => {
    router.post(route('logout'));
};
</script>
<script>
export default {
  data() {
    return {
      menuOpen: false
    };
  },
  methods: {
    toggleMenu() {
      this.menuOpen = !this.menuOpen;
    },
    closeMenu() {
      this.menuOpen = false;
    }
  }
};
</script>
<style scoped>
/* General styles */
header {
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 10px 20px;
}

.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo a {
  font-size: 24px;
  font-weight: bold;
  text-decoration: none;
  color: #333;
}

/* Desktop menu styles */
.desktop-menu {
  display: none;
}

.desktop-menu ul {
  list-style: none;
  display: flex;
  margin: 0;
  padding: 0;
}

.desktop-menu ul li {
  margin-left: 20px;
}

.desktop-menu ul li a {
  text-decoration: none;
  color: #333;
  font-size: 18px;
  transition: color 0.3s;
}

.desktop-menu ul li a:hover {
  color: #007BFF;
}

/* Hamburger icon styles */
.hamburger {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  width: 30px;
  height: 30px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
  z-index: 10;
}

.hamburger-bar {
  width: 100%;
  height: 3px;
  background-color: #333;
  border-radius: 2px;
  transition: all 0.3s;
}

/* Mobile menu styles */
.mobile-menu {
  position: fixed;
  top: 0;
  right: -100%;
  width: 250px;
  height: 100%;
  background-color: #fff;
  transition: right 0.3s ease-in-out;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  z-index: 999;
}

.menu-open {
  right: 0;
}

.mobile-menu ul {
  list-style: none;
  padding: 0;
  margin: 60px 0 0 0;
}

.mobile-menu ul li {
  padding: 15px 20px;
  border-bottom: 1px solid #f0f0f0;
}

.mobile-menu ul li a {
  text-decoration: none;
  color: #333;
  font-size: 18px;
  display: block;
}

/* Overlay styles */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  z-index: 998;
}

/* Responsive styles */
@media (min-width: 768px) {
  .desktop-menu {
    display: flex;
  }

  .hamburger {
    display: none;
  }

  .mobile-menu {
    display: none;
  }
}
</style>




<template>
   
        <Head :title="title" />

        <Banner />
        <div>
    <header>
      <div class="container">
        <!-- Logo -->
        <div class="logo">
          <inertia-link href="/">MySite</inertia-link>
        </div>

        <!-- Desktop Menu -->
        <nav class="desktop-menu">
          <ul>
            <li><inertia-link href="/">خانه</inertia-link></li>
            <li><inertia-link href="/about">درباره ما</inertia-link></li>
            <li><inertia-link href="/services">خدمات</inertia-link></li>
            <li><inertia-link href="/contact">تماس با ما</inertia-link></li>
          </ul>
        </nav>

        <!-- Hamburger Icon for Mobile -->
        <button @click="toggleMenu" class="hamburger">
          <span class="hamburger-bar"></span>
          <span class="hamburger-bar"></span>
          <span class="hamburger-bar"></span>
        </button>

        <!-- Mobile Menu -->
        <nav :class="{ 'menu-open': menuOpen }" class="mobile-menu">
          <ul>
            <li><inertia-link href="/" @click="closeMenu">خانه</inertia-link></li>
            <li><inertia-link href="/about" @click="closeMenu">درباره ما</inertia-link></li>
            <li><inertia-link href="/services" @click="closeMenu">خدمات</inertia-link></li>
            <li><inertia-link href="/contact" @click="closeMenu">تماس با ما</inertia-link></li>
          </ul>
        </nav>
      </div>
    </header>
    <div v-if="menuOpen" class="overlay" @click="closeMenu"></div>
  </div>


</template>
