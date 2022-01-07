# Redux saga

# Giới thiệu tổng quan về redux-saga

- `Redux` là thư viện quản lý state cấp độ global

- `Redux middleware` là tầng đứng giữa `action` và `reducer`, trước khi action được truyền vào reducer sẽ đi qua tầng này và thực hiện các chức năng cần thiết

- Một vài redux middleware thường hay sử dụng:
    
    - Redux logger

    - Redux thunk

    - Redux saga

- `Redux saga` là một middleware của redux dùng để quản lý các side-effects


# Cài đặt

- Cài đặt thư viện redux-saga

> ## yarn add redux-saga

- Khởi tạo rootSaga: rootSaga là nơi quản lý toàn bộ các saga con

```jsx
    import { call, put, takeEvery, takeLatest } from 'redux-saga/effects'
    import Api from '...'

    // worker Saga: will be fired on USER_FETCH_REQUESTED actions
    function* fetchUser(action) {
        try {
            const user = yield call(Api.fetchUser, action.payload.userId);
            yield put({type: "USER_FETCH_SUCCEEDED", user: user});
        } catch (e) {
            yield put({type: "USER_FETCH_FAILED", message: e.message});
        }
    }

    /*
        Starts fetchUser on each dispatched `USER_FETCH_REQUESTED` action.
        Allows concurrent fetches of user.
    */
    function* mySaga() {
        yield takeEvery("USER_FETCH_REQUESTED", fetchUser);
    }

    export default mySaga;
```

- Cài đặt saga vào redux

```jsx
    import { createStore, applyMiddleware } from 'redux'
    import createSagaMiddleware from 'redux-saga'

    import reducer from './reducers'
    import mySaga from './sagas'

    // create the saga middleware
    const sagaMiddleware = createSagaMiddleware()
    // mount it on the Store
    const store = createStore(
        reducer,
        applyMiddleware(sagaMiddleware)
    )

    // then run the saga
    sagaMiddleware.run(mySaga)

    // render the application

```


# Bài tập


1. Làm chức năng cart 

    - add to cart

    - increment/decrement

    - remove items

    - view cart

    GET_CART

2. Login get profile, get cart

    - B1: Login

    - B2: Get profile, cart

3. Logout clear cart