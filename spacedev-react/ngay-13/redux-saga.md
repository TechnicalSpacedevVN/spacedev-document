# Redux saga

- Là một middleware cho redux chuyên để xử lý side effect hiệu quả.

- Redux saga mạnh mẽ khi xử lý side effect phức tạp

- Redux saga và redux thunk cùng có thể xử lý slide effect (call api, xử lý side effect ko liên quan tới state). Nhưng redux saga có những công cụ cho phép xử lý hiệu quả hơn redux thunk.

- Nếu dự án nhỏ và trung bình, hoặc không có case nào phức tạp thì redux thunk vẫn xử lý ổn. Tuy nhiên sẽ rất phức tạp nếu redux thunk xử lý những case sau đây:

# Hướng dẫn sử dụng

Bước 1: Cài đặt thư viện redux-saga

> yarn add redux-saga


Bước 2: Tạo ra một cartSaga dùng cho chức năng cart

```jsx
    import { createAction, createSlice } from "@reduxjs/toolkit";
    import { call, takeLatest, put, delay } from 'redux-saga/effects'

    export const { reducer: cartReducer, actions: cartActions, name } = createSlice({
        name: 'cart',
        initialState: {
            cart: null,
            openCartOver: false
        },
        reducers: {
            setCart: (state, action) => {
                state.cart = action.payload
            },
            toggleCartOver: (state, action) => {
                state.openCartOver = action.payload
            }
        }
    })

    // function action
    export const updateCartItemAction = createAction(`${name}/addCart`)

    // Function saga sẽ được thực thi khi có 1 action được thực thi
    function* fetchUpdateCartItem(action) {
        try {
            // delay 200ms, khi user click nhanh sẽ không thực thi api
            yield delay(200)

            // Thực thi api `updateProduct`. Các tham số sẽ được truyền phía sau 
            yield call(cartService.updateProduct, action.payload.productId, action.payload.quantity)

            // put tương tự dispatch
            yield put(getCartAction())
            
            if (action.payload.showPopover) {
                yield put(cartActions.toggleCartOver(true))
                window.scroll({
                    top: 0,
                    behavior: 'smooth'
                })
            }

        } catch (err) {
            console.error(err)
        }
    }

    // root Saga
    export function* cartSaga() {
        // Lắng nghe khi user thực thi `updateCartItemAction`, fetchUpdateCartItem sẽ được thực thi
        yield takeLatest(updateCartItemAction, fetchUpdateCartItem)
    }

```

Bước 3: Cài đặt saga middleware vào redux store

```jsx
    // ./stories/index.jsx
    import { configureStore } from "@reduxjs/toolkit";
    import { authReducer, getUserThunkAction } from "./auth";
    import { ENV } from "@/config";
    import { cartReducer, cartSaga, getCartAction } from "./cart";
    import createSagaMiddleware from 'redux-saga'
    import { all } from "redux-saga/effects";

    // Tạo ra một rootSaga, giống như reduxer, trong trường hợp có nhiều saga chúng ta cần tạo ra một rootSaga
    function* rootSaga() {
        yield all([
            cartSaga(),
            // Thêm những saga dành cho những reducer khác ở đây
        ])
    }

    // Tạo ra 1 saga middleware
    const saga = createSagaMiddleware()

    export const store = configureStore({
        reducer: {
            auth: authReducer,
            cart: cartReducer
        },
        middleware: (getDefaultMiddlware) => getDefaultMiddlware().concat(saga), // Gắn saga vào trong redux
        devTools: ENV === 'development'
    })

    // Khởi chạy saga middleware
    saga.run(rootSaga)
```

# Một vài function thường sử dụng

- `put`: Giống dispatch

- `putResolve`: Giống dispatch nhưng chờ kết quả trả về

- `call`: Để thực thi một Promise

- `takeLatest`: Thực thi action cuối cùng, trong quá trình thực hiện action mà có cùng action đó được thực thi thì action cũ sẽ được cancel

- `takeEvery`: Thực thi tất cả actio0n

- `delay`: delay 1 khoảng thời gian (Giống delay sử dụng promise, nhưng delay này chỉ sử dụng cho function generator)


# Case study

Ngoại trừ những case xử lý side effect call api, loading bình thường thì redux-saga sẽ mạnh hơn redux-thunk ở những case sau đây:

- Chỉ thực hiện action cuối cùng khi user thao tác nhanh và cancel những action trước đó

- Delay các action

- Xử lý thông tin user và cart với những logic phức tạp:

    1. Xử lý khi user logout ngay sau khi login

    2. Xử lý khi refresh page, cart chưa lấy về kịp thì user logout



# So sánh redux-saga và redux-thunk

1. Redux-saga

    Khó tiếp cận, cần cài đặt thư viện
    
    Xử lý những case phức tạp đơn giản

    Dùng nhiều trong các dự án có logic phức tạp

    Không tận dụng được cơ chế dispatch async/await do @reduxjs/toolkit hỗ trợ. xử lý loading phức tạp


2. Redux-thunk

    Dễ hiểu, dễ tiếp cận

    Được @reduxjs/toolkit hỗ trợ sẵn, không cần phải cài đặt thêm thư viện

    @reduxjs/toolkit hỗ trợ cơ chế xử lý bất đồng bộ khi dispatch trong component, dễ dàng trong xử lý loading


# Function generator

Function generator là một loại function trong javascript mà có thể dùng để tạo ra các iterator. Ví dụ sau sẽ giúp cho bạn hiểu cách sử dụng function generator: (Funtion generator tự động return về 1 Generator giống async tự động trả về 1 promise)


```jsx
    function* countUpTo(max) {
        let count = 1;
        while (count <= max) {
            yield count;
            count++;
        }
    }

    const iterator = countUpTo(5);
    console.log(iterator.next().value); // 1
    console.log(iterator.next().value); // 2
    console.log(iterator.next().value); // 3
    console.log(iterator.next().value); // 4
    console.log(iterator.next().value); // 5
    console.log(iterator.next().value); // undefined
```

Trong ví dụ trên, chúng ta đã tạo một function generator `countUpTo` nhận vào một tham số `max`. Function này sẽ tạo ra một iterator với các giá trị từ 1 đến `max`. Sử dụng `yield` trong function generator cho phép ta trả về giá trị hiện tại và tiếp tục chạy function khi gọi `next()` trên iterator.

Bạn có thể sử dụng function generator để tạo ra các iterator cho các vòng lặp, hoặc để thực hiện các tác vụ dài và cần phải tạm dừng trong quá trình thực hiện.

Function generator cung cấp một cách dễ dàng để quản lý các tác vụ bất đồng bộ và cho phép bạn tạo ra các iterator để lặp qua các giá trị trả về.