<template>
  <div>
    <section class="main">
      <input
        id="toggle-all" 
        class="toggle-all"
        type="checkbox"
        :checked="remaining === 0"
        @change="toggleAll" />
        <label for="toggle-all">Mark all as complete</label>
        <!-- v-show="todos.length" -->
    </section>
  </div>
</template>

<script>
export default {
}
</script>

<style scoped>
.main {
	position: relative;
	z-index: 2;
	border-top: 1px solid #e6e6e6;
}
.toggle-all{
  content: '❯';
  display: inline-block;
  font-size: 3rem;
  color: #949494;
  padding: 1rem 1rem 1rem 1rem;
  -webkit-transform: rotate(90deg);
  transform: rotate(90deg);
}
/* toggle-all label은 클릭하기 전에는 보이면 안되고, 클릭했을때만 보이게 해야함 */
/* toggle-all을 포함하고 있는 네모칸도 클릭했을때 주변 테두리 들어갈 수 있도록 하기*/
.toggle-all + label{
  display: flex;
  align-items: center;
  justify-content: center;
  width: 2rem;
  height: 5rem;
  font-size: 0;
  position: absolute;
  top: 2rem;
  left: -0;
}
/* .toggle-all:focus-within {
  content: '❯';
  display: inline-block;
  font-size: 3rem;
  color: #949494;
  padding: 1rem 1rem 1rem 1rem;
  -webkit-transform: rotate(90deg);
  transform: rotate(90deg);
} */
.toggle-all:checked + label:before {
  color: #d91111;
  border-color: red;
}
.toggle-all + label:before {
	content: '❯';
	display: inline-block;
	font-size: 22px;
	color: #949494;
	padding: 10px 27px 10px 27px;
	-webkit-transform: rotate(90deg);
	transform: rotate(90deg);
}
</style>
