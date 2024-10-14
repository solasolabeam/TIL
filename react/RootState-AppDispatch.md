# RootState 와 AppDispatch


## RootState
> RootState는 Redux 스토어의 전체 상태를 나타내는 타입, 스토어에서 관리하는 모든 리듀서의 상태들이 합쳐진 타입을 정의하는 것

```javascript
export type RootState = ReturnType<typeof store.getState>;
```

- ReturnType<typeof store.getState>는 스토어의 getState 함수가 반환하는 값의 타입을 자동으로 추론하는 역할을 함. 즉, 스토어의 상태 구조를 기반으로 RootState를 정의하여 타입스크립트가 상태의 정확한 구조를 알 수 있도록 정의하는 것

- 이 타입은 Redux 상태에 접근하는 함수나 컴포넌트에서 사용되고, useSelector를 사용할 때 RootState 타입을 명시함으로써 상태의 특정 부분을 안전하게 선택할 수 있습니다.
  
#### 예시
```javascript
import { useSelector } from 'react-redux';
import { RootState } from '../store';

const MyComponent = () => {
  const counter = useSelector((state: RootState) => state.counter.value);
  
  return <div>{counter}</div>;
};

```
  
  
## AppDispatch
  
> AppDispatch는 Redux의 dispatch 함수의 타입을 나타냄. store.dispatch 함수는 리덕스에서 액션을 디스패치할 때 사용되며, 이 함수의 타입을 AppDispatch로 정의.
  
```javascript
export type AppDispatch = typeof store.dispatch;
```
  
  
- AppDispatch는 스토어의 dispatch 함수 타입을 자동으로 가져와서 저장하고, 주로 dispatch를 사용할 때 해당 함수가 어떤 액션을 허용하는지 TypeScript에서 추론할 수 있도록 도와줌.

- 특히 Redux Thunk 같은 비동기 미들웨어를 사용할 때, dispatch가 비동기 액션도 처리할 수 있다는 것을 타입 시스템에 알려주기 위해 정의.
  
#### 예시
```javascript
import { useDispatch } from 'react-redux';
import { AppDispatch } from '../store';
import { increment } from '../features/counter/counterSlice';

const MyComponent = () => {
  const dispatch = useDispatch<AppDispatch>();

  const handleIncrement = () => {
    dispatch(increment());
  };

  return <button onClick={handleIncrement}>Increment</button>;
};
```

##   결론
  
- RootState: Redux 스토어의 전체 상태 타입을 정의하고 컴포넌트에서 Redux 상태를 선택하거나 접근할 때 사용.

- AppDispatch: Redux의 dispatch 함수 타입을 정의하고. 액션을 디스패치할 때 해당 액션의 타입을 안전하게 처리할 수 있도록 정의하는것.