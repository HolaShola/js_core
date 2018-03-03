import { parse } from 'query-string';

console.log(window.location.search);
>>> ?nodeID=2141

console.log(parse(window.location.search));
>>> {nodeID: "2141"}

const { nodeID: accountID } = parse(window.location.search);
// const { nodeID: accountID } = {nodeID: "2141"}

>>> accountID
>>> "2141"

//----------------------------------------------

reselect for redux https://medium.com/devschacht/neil-fenton-improving-react-and-redux-performance-with-reselect-40f1d3efba89

import { createSelector } from 'reselect';

export const getItems = (state) => state.cart.get('items');

export const getItemsWithTotals = createSelector(
    [ getItems ],
    (items) => {
        return item.map(i => {
            return i.set('total', i.get('price', 0) * i.get('quantity'));
        });
    }
);

Первая функция просто получит все элементы в корзине, а вторая функция является мемоизированным селектором. Reselect предоставляет createSelector API, позволяющий нам создать мемоизированный селектор. Это означает, что getItemsWithTotals будет вычисляться при первом запуске функции. Если эта же функция вызывается снова, но входные данные (результат getItems) не изменились, функция просто вернет кешированный расчет элементов и их итогов. Если элементы изменены (например, добавлен элемент, изменилось количество, любые манипуляции с результатом getItems), функция снова будет выполнена.