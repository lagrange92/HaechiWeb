<template>
  <div class="directions">
    <div class="dropdown">
      <button class="dropdown-button">길찾기</button>
      <div class="dropdown-content">
        <p>Dropdown 1</p>
        <p>Dropdown 2</p>
        <p>Dropdown 3</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "RouteMenu",
};
</script>

<style>
.directions {
  padding: 10px;
}

.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown-button {
  background-color: transparent;
  border: none;
  cursor: pointer;
}

.dropdown-content {
  display: none;
  position: absolute;
  z-index: 1;
  background-color: #f1f1f1;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  padding: 12px 16px;
}

.dropdown:hover .dropdown-content {
  display: block;
}
</style>
