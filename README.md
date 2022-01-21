### index.js
```
import { createStore, applyMiddleware } from 'redux'
import createSagaMiddleware from 'redux-saga'

import  paymentSaga  from './sagas/paymentSaga.js'

const sagaMiddleware = createSagaMiddleware()
const store = createStore(
  reducer,
  applyMiddleware(sagaMiddleware)
)
sagaMiddleware.run(paymentSaga)

```

### sagas/paymentSaga.js
```
    import {call, put, takeLatest} from 'redux-saga/Effects';


    function* paymentConfirmation(action) {
        try{
            const paymentConfirmation = yield call(Api.fetchPaymentConfirmation, action.payload.payments );
            yield put({type: PaymentAction.success, payments: paymentConfirmation})
        } catch(e) {
            yield put({type: PaymentAction.failed, e})
        }
    }

    function* paymentSaga() {
        yield takeLatest(PaymentAction.initialised, paymentConfirmation)
    }
```
