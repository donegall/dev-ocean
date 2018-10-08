# Squid API
## This is the New API, the old ones are listed at the bottom

## Ocean
- Ocean(config(web3Provider, nodeURI, gas, network, providerURI))
- getInstance()
- getAccounts() => list of accounts along with token and eth balances
- getTokenBalance()
- getEthBalance()
- requestTokens(amount) => bool
- getMessageHash(message) => hash of the given message
- generateDID(content) => ocean specific DID with a random id based on the given string message
- resolveDID(did) => DDO of the given DID

## Order
- purchaseAsset(assetDID, publisherId, price, timeout)
- getOrderStatus(orderId) => integer representing the order status as defined in the keeper 
- getOrders() => list of orders
- verifyOrderPayment(orderId) => true / false

## Asset / Metadata
- publishDataAsset(assetDID, assetDDO, price)
- updateAsset(assetDDO)
- retireAsset(assetDID)
- getAssets() => asset ids from keeper
- checkAsset(assetDID) => true / false
- getAssetPrice(assetDID)
- getAssetMetadata(assetDID) => asset DDO
- getAssetsMetadata(<search-params>) => list of assets DDOs

## Provider
- registerProvider(url, provider_address)
- getProviders()
- getAssetProvider(assetDID)


# Old squid API

## Ocean
- `js` Ocean(config(web3Provider, nodeUri, gas, network, providerUri))
- `js` getInstance()
- `js` getAccounts()
- `js` getOrdersByConsumer(consumerAddress)
- `js` purchaseAsset(assetId, publisherId, price, privateKey, publicKey, timeout, senderAddress, initialRequestEventHandler, accessCommittedEventHandler, tokenPublishedEventHandler)

### Token
- `py` approve(address, resource_price)
- `py` getBalance(account)
- `js` getTokenBalance(accountAddress)
- `js` getEthBalance(account)

### Market
- `py` generateID(content)
- `py` verifyOrderPayment(orderId)
- `js` verifyOrderPayment(orderId) 
- `py` register(name, description, price, publisherAddress)
- `js` registerAsset(name, description, price, publisherAddress)
- `py` requestTokens(amount, address)
- `js` requestTokens(amount, address)
- `py` sendPayment(assetId, order, publisherAddress, senderAddress)
- `js` payAsset(assetId, order, publisherAddress, senderAddress)
- `py` checkAsset(assetId)
- `js` checkAsset(assetId)
- `py` getAssetPrice(assetId)
- `js` getAssetPrice(assetId)

### `py` Acl `js` Auth
- `py` getOrderStatus(orderId)
- `js` getOrderStatus(orderId) 
- `py` initiateAccessRequest(resourceID, providerAddress, pubKey, timeout)
- `py` commitAccessRequest(id, isAvailable,  expirationDate,  discovery,  permissions,  accessAgreementRef,   accessAgreementType)
- `py` deliverAccess Token(id, encryptedAccessToken)
- `py` getEncryptedAccessToken(orderId, senderAddress)
- `js` getEncryptedAccessToken(orderId, senderAddress)
- `py` cancelAccessRequest(orderId, senderAddress)
- `js` cancelAccessRequest(orderId, senderAddress)

### `py` Web3 `js` helper
- `py` sign(accountAddress, message)
- `js` sign(accountAddress, message)
- `py` getMessageHash(message)
- `py` toChecksumAddress(address)
- `py` toHex()
- `py` toBytes()
- `js` getAccounts()

### Metadata
- `py `getAssetMetadata(assetId)
- `py` getAssets()
- `py` getAsstesMetadata()
- `js` getAssetsMetadata()
- `py` publishAsset(providerId, assetId, publisherId, name, size, author, license, contentType, contentUrls, price, *)
- `js` publishDataAsset(asset)
- `py` updateAsset(providerId, assetId, publisherId, name, size, author, license, contentType, contentUrls, price, *)
- `py `retireAsset(providerId, assetId)

### Providers
- `py` registerProvider(url, provider_address)
- `py` getProviders()
- `py` getAssetProvider(assetId)

# Examples

List orders in JavaScript

```javascript
import { Ocean } from '@oceanprotocol/squid'

const ocean = await new Ocean({network: 'kovan'})
const orders = ocean.getOrdersByConsumer('0x970e8f18ebfEa0B08810f33a5A40438b9530FBCF')

console.log(orders)
```

Access market functionality in JavaScript

```javascript
import { Ocean } from '@oceanprotocol/squid'

const ocean = await new Ocean({network: 'kovan'})
const { market } = ocean

await market.verifyOrderPayment('0x970e8f18ebfEa0B08810f33a5A40438b9530FBCF')
```