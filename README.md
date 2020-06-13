#### Redux Integration in React JS
- First of all add 'Action Type' (Just type of operation you are going to perform for eg. in e-commercial website we have to add the product price so we will make unique name for this  *action type* i.e PRODUCT_ADD).
- In second step we have to create 'Action' (basically it describe that what is going to happen inside this process).**From component we generally call Action method to process the functionality beacuse it is responsible to run the reduce function. Generally we use the below code to call the functionality from the repective component.***
```javascript
   dispatch(addProduct)
``` 
- In the End we have to make the 'Reducer'  file where we actually write the logic to perform the operation.


######  Lets  discuss the implementation of the reducer in react js with example:-

We are making the redux for shop to make the count of the cake after each sell.


1.  Create the  'Action Type' as discussed.
```javascript
//cakeType.js
export const BUY_CAKE = 'BUY_CAKE'
```

2. Now Create the 'Action'  for the above 'Action Type'.
```javascript
//cakeActions.js
import { BUY_CAKE } from './cakeTypes';
export const buyCake = (number = 1) => {
  return {
    type: BUY_CAKE,
    payload: number
       }
  }
```

3. Now create the 'Reucer' the main logic.

```javascript
//cakeReducer.js
import { BUY_CAKE } from './cakeTypes';

const initialState = {
  numOfCakes: 10
}

const cakeReducer = (state = initialState, action) => {
  switch (action.type) {
    case BUY_CAKE: return {
      ...state,
      numOfCakes: state.numOfCakes - action.payload
    }

    default: return state
  }
}

export default cakeReducer
```

#### Now how we can make make use inside component.
1. If we have to take the data from the Redux state the we have to use:-
```javascript
mapStateToProps
```
2. When call the methods of the reducer then we have to use:-
```javascript
mapDispatchToProps
```
3. For the communication among component, mapStateToProps and mapDispatchToProps. We have to use the *connect*  from below import : -
```javascript
import { connect } from 'react-redux'
```

Now lets complete the above example from the working of the component that will use the aboue as the redux methods.
```javascript
import React from 'react'
import { connect } from 'react-redux'
import { buyCake } from '../redux'

function CakeContainer (props) {
  return (
    <div>
      <h2>Number of cakes - {props.numOfCakes} </h2>
      <button onClick={props.buyCake}>Buy Cake</button>
    </div>
  )
}

const mapStateToProps = state => {
  return {
    numOfCakes: state.cake.numOfCakes
  }
}

const mapDispatchToProps = dispatch => {
  return {
    buyCake: () => dispatch(buyCake())
  }
}

export default connect(mapStateToProps,mapDispatchToProps)(CakeContainer)
```





