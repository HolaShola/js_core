import { parse } from 'query-string';

console.log(window.location.search);
>>> ?nodeID=2141

console.log(parse(window.location.search));
>>> {nodeID: "2141"}

const { nodeID: accountID } = parse(window.location.search);
// const { nodeID: accountID } = {nodeID: "2141"}

>>> accountID
>>> "2141"