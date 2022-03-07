# Submission - By Mohammad Kawadri: 

#### Note:
- Having looked at the package.json and finding that Vue is set to "vue": "^2.5.2", means that we are using Vue 2, and therefore we will continue using the Vue options data API to modify and build components. 
* `More information found at https://v2.vuejs.org/v2/api/?redirect=true#Options-Data`
- I did not upgrade Vue 2 to Vue 3, because this was not requested in the spec, and in a working environment, this may disrupt other users and or production code. 

- Apologies for the second git commit on MASTER containing all the project files, additional to the changes I made. I was using VS code to push changes to Github, and for some reason, the initial commit did not push all the files though. All subsequent pushes were made through Atlassian sourcetree. 

## Optimisations and comments: 
#### App.vue
1. Set Min = 0 and Max = 100 ranges for the number input tag. The Spec mentions that only 1 to 100 should appear on the screen as a user input. 

2. Set v-model to v-model.number in the input tag, so that the result is returned as typeof(Number) === true.

3. Set up a computed method to listen, update, and return the "limit" change from 100 when modified by user.

4. Passed "number" prop to the "Numbers" component, passing through the value returned from the getLimit computed method I created. 

*3. & 4.* Set up a computed method to pass reactive data from parent to child, this is less expensive on Vue engine than using a watch option to listen to parent!
* `Please see https://v2.vuejs.org/v2/guide/computed.html?redirect=true for more information.`

#### Numbers.vue
1. Renamed "n()" in the methods option, and also changed "v-for="number in n()"" to  "v-for="number in "listOfRandomisedNumbers()". "n()" is not a maintainable or descriptive name for any function / method. I changed it so its more descriptive and maintainable. 

2. Created a props option, and validated the prop type, expecting the prop to return type Number.
 `https://v2.vuejs.org/v2/api/?redirect=true#props`  
 

3. Deleted watch option from script, since we are receiving the "number" prop that automatically returns the input value from the parent component. 

4. In the "listOfRandomisedNumbers()" method, I changed i = 0 to ...... i = 1, since the numbers should start at 1, and not 0. 

5. I also changed "i < this.limit" to ...... "i < (this.$props.number + 1)" so that we get a list of 1-100 rather than 0-99. 

6. Renamed "n()" to "listOfRandomisedNumbers()" since function needed to return random numbers. 

7. "listOfRandomisedNumbers()" did not have an efficient Math.Random function, as it had a bias of only 0.5. I implemented a randomise "for loop" Algorithm known as the "Fisher–Yates shuffle".

8. see git MASTER commit "set this.$data.numbers..." \ Deleted $data.numbers, since number is being provided as a reactive state via $props. No need for duplication of reactive state in child from parent. 

9. Renamed "hov" method to "highlight" so its more descriptive to what the function does. 

10. line 35, changed nums variable to use Vue Virtual dom $refs, rather than the this.window DOM method, that used document queries and selectors. 

11. line 38, got values for each number using "innerText".

\ * `Reference: Fisher–Yates shuffle www.geeksforgeeks.org/shuffle-a-given-array-using-fisher-yates-shuffle-algorithm/`

### Spec
Using Vue, display all numbers from 1 to 100 in a random order on the screen. This number should be configurable via a provided input box.
If the user places their pointer over a given number, highlight that numbers' divisors.
For example, if the user hovers over 21, the numbers 1, 3, 7 would be highlighted. 22 would highlight 1, 2 and 11.

### Interview Task
The provided code is functional, but it's got some issues that need to be resolved. These issues may or may not be logical in nature - just because the code is working doesn't necessarily mean it is the best way of doing something.

Improve the code how you see fit - please leave comments to justify your decisions.

### GitHub Pull Requests
This is an interview task sent to prospective candidates to work at Aluminati. As such, all pull requests will be rejected. This code is, by its very nature, purposely designed with issues that candidates are asked to review!

If you have been invited to perform this test your submission should be through your point of contact with us, e.g. your recruitment agency.


