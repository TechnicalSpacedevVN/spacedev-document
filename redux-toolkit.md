# @reduxjs/toolkit

1. Redux toolkit là thư viện giúp cho việc viết code redux trở nên dễ dàng hơn, được team redux phát triển và khuyên dùng

2. Mặc định redux toolkit cài đặt sẵn thunk

3. `createSlice`: Tạo ra một slice object giúp cho việc viết code redux dễ dàng hơn:

    1. Input:

        - `name`: tên của reducer

        - `initialState`: giá trị mặc định, có thể nhận vào giá trị hoặc callback return về giá trị

        - `reducers`: Các case thay đổi state

        - `extraReducers`: Cũng là các case thay đổi state, nhưng sẽ không dùng để generate actions. Thường dùng để xử lý bất đồng bộ, side effect

    2. Output

        - `reducer`: function redducer

        - `actions`: Được generate từ reducers
        
        - `name`: Tên của reducer

        - `getInitialState`: Lấy ra initialState, trong trường hợp initialState là 1 callback, thực thi callback và lấy ra giá trị



4. `createAction`: Tạo ra một function action

5. `createAsyncThunk`: Tạo ra một function action sử dụng thunk

    1. Input:

        - `typePrefix` - string: action name

        - `payloadCreator` - AsyncThunkPayloadCreator: (`payload`, `thunkApi`) => any

            - thunkApi: Chứa các thunk api tiện dụng: fulfillWithValue, rejectWithValue, abort, dispatch,....

    2. Output: AsyncThunk





# Lợi ích khi sử dụng @reduxjs/toolkit

1. Setup đơn giản hơn

2. Bật tắt devtool dễ dàng

3. Xử lý async function đơn giản nhờ thunk và unwrap / unwrapResult

4. Tự động cài đặt thunk

5. Tự động generate function action, xử lý action name
