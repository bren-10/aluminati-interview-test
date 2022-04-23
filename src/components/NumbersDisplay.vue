<template>
  <div>
    <div class="number" :id="'number-' + number" v-for="number in n()" :key="number" @mouseover="onHover(number)" @mouseout="reset">
      {{number}}
    </div>
  </div>
</template>

<script>
export default {
  name: "NumbersDisplay", // Noticed documentation stating to specifically declare a 'name' for the component here.
  // Also, Vue complains when a component's name is only a single word, hence the change to 'NumbersDisplay'.
  data()
  {
    return {
      limit: this.$parent.limit,
      numbers: []
    }
  },
  watch: {
    ["$parent.limit"](newLimit) {
      this.limit = newLimit;
    }
  },
  methods: {

    n() {
      let numbers = [];
      for (let i = 0; i < this.limit; i++) {
        // numbers = [...numbers, i];
        // Pushing to list instead, as it's easier to read.
        numbers.push(i)
      }

      // (Personal preference) Instead of returning logic directly, return a variable instead.
      const randomisedNums = numbers.sort(() => Math.random() - 0.5);
      return randomisedNums
      
      // ** I've learnt that reverse while loops are slightly faster performance-wise.
      // ** Considering the user might want to generate a large quantity of numbers, 
      // ** saving some delay wherever possible might be beneficial (albeit a small difference).
      // ** For what it's worth, here is the same functionality using a reverse while loop (unused):

      // let numbers = [];
      // let lim = this.limit
      // while (lim--) {
      //   numbers.push(lim)
      // }
      
      // const randomisedNums = numbers.sort(() => Math.random() - 0.5);
      // return randomisedNums
    },
    
    onHover(number) {
      const nums = document.querySelectorAll('.number');

      for (let i = 0; i < nums.length; i++) {
        const num = nums[i].textContent; // Removed .trim(), not needed because n() does not generate whitespace.
        if (number % num === 0) { // Automatically converts string to int for calculation
          nums[i].classList.add('active')
          // console.log('divisor', num)
        }
      }

      // * See comments marked with ** n() above (reverse while loop for performance)
      // * Example of the same functionality using reverse while loop (unused):

      // let numLength = nums.length
      // while (numLength--){
      //   const num = nums[numLength].textContent;
      //   if (number % num === 0) {
      //     nums[numLength].classList.add('active')
      //   }
      // }
    },

    reset() {
      const nums = document.querySelectorAll('.number');
      nums.forEach(num => num.classList.remove('active'))
    }

  }
}
</script>

<style scoped>

  /* Made some minor overall styling improvements */
  
	.number {
		display: inline-block;
		padding: 8px;
		background-color: lightgrey;
		margin: 5px;
    border-radius: 50%;
	}

  /* Reset cursor on hover */
	.number:hover {
		cursor: default;
	}

	.active {
		background-color: red;
	}
</style>
