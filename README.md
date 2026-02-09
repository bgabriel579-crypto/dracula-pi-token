# Pi Network Token Creator

A complete solution for creating tokens on the Pi Network Testnet based on the official Pi Network documentation.

## 📋 Prerequisites

1. **Two Pi Wallet Testnet Accounts**
   - One will be the **Issuer** (creates the token)
   - One will be the **Distributor** (receives the initial supply)
   - Both must be activated on Pi Testnet

2. **Private Keys**
   - Get the private keys from Pi Wallet settings
   - Never share these keys with anyone!

3. **Domain (Optional but recommended)**
   - For listing in Pi Wallet, you need a domain
   - The domain must support HTTPS

## 🚀 Quick Start

### 1. Configure Your Wallet Keys

Edit `create-token.js` and update the `WALLET_CONFIG`:

```javascript
const WALLET_CONFIG = {
  issuerSecret: "SXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX", // Your issuer private key
  distributorSecret: "SXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" // Your distributor private key
};
```

### 2. Configure Token Details

Update the `TOKEN_CONFIG` in `create-token.js`:

```javascript
const TOKEN_CONFIG = {
  code: "MYTOKEN",           // Token code (max 12 characters, alphanumeric)
  name: "My Token",          // Display name
  description: "My custom token on Pi Network", // Description
  totalSupply: "1000000",    // Total supply to mint
  homeDomain: "yourdomain.com", // Your domain
  image: "https://yourdomain.com/token-icon.png" // Token icon URL
};
```

### 3. Create the Token

```bash
# Create the token
node create-token.js create

# Check if token exists
node create-token.js check
```

## 📝 Process Explained

### Step 1: Trustline Creation
The distributor wallet establishes a trustline to the new token. This is the first time the token is recognized on-chain.

### Step 2: Token Minting
The issuer sends tokens to the distributor, effectively creating (minting) the tokens.

### Step 3: Home Domain Setup
The issuer sets a home domain, which links the token to a website for validation.

### Step 4: pi.toml Configuration
Host a `pi.toml` file at `https://yourdomain.com/.well-known/pi.toml` with token metadata.

## 🔧 Configuration Files

### pi.toml Template

```toml
[[CURRENCIES]]
code="MYTOKEN"
issuer="GXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
name="My Token Name"
desc="Description of my token"
image="https://yourdomain.com/token-icon.png"
```

**Required Fields:**
- `code`: Token code (alphanumeric, max 12 chars)
- `issuer`: Public key of the issuer account
- `name`: Token issuer name
- `desc`: Token description
- `image`: URL to token icon (must be HTTPS)

## 🌐 Hosting Requirements

For your token to appear in Pi Wallet:

1. **HTTPS Required**: All URLs must use HTTPS
2. **Accessible Files**: Both `pi.toml` and token image must be publicly accessible
3. **Content-Type**: `pi.toml` must be served as `text/plain`
4. **Caching**: Ensure proper caching for reliability

## 📊 Token Verification

After creation, you can verify your token:

```bash
# Check token status
node create-token.js check

# Or visit the URL directly
https://api.testnet.minepi.com/assets?asset_code=MYTOKEN&asset_issuer=YOUR_ISSUER_PUBLIC_KEY
```

## ⚠️ Important Notes

- **Testnet Only**: This is for Pi Testnet only
- **No Real Value**: Testnet tokens have no real value
- **Security**: Never commit private keys to version control
- **Validation**: Pi Server scans tokens regularly; invalid configurations may be delisted

## 🔍 Troubleshooting

### Common Issues

1. **"Running scripts is disabled"**
   ```bash
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```

2. **Transaction Failed**
   - Check if accounts have enough Test-Pi for fees
   - Verify private keys are correct
   - Ensure accounts are activated on testnet

3. **Token Not Appearing in Wallet**
   - Verify `pi.toml` is accessible via HTTPS
   - Check all required fields are present
   - Wait for Pi Server to scan (can take time)

## 📚 Additional Resources

- [Pi Network Token Documentation](https://github.com/pi-apps/pi-platform-docs/blob/master/tokens.md)
- [Stellar Documentation](https://developers.stellar.org)
- [Stellar JS SDK](https://stellar.github.io/js-stellar-sdk)
- [Token Best Practices](https://developers.stellar.org/docs/tokens/how-to-issue-an-asset)

## 🛡️ Security Best Practices

1. **Never share private keys**
2. **Use environment variables for sensitive data**
3. **Test with small amounts first**
4. **Keep your Node.js dependencies updated**
5. **Use HTTPS for all external resources**

## 📞 Support

If you encounter issues:
1. Check the Pi Network documentation
2. Verify your configuration
3. Ensure you're using Testnet
4. Check transaction details on Pi Testnet explorer
