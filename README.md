# Financial Trading Simulation

## Klassendiagramm

```mermaid
classDiagram
    class User {
        -String username
        -double balance
        -List<Stock> ownedStocks
        +buyStock(stock: Stock, quantity: int): void
        +sellStock(stock: Stock, quantity: int): void
    }

    class Stock {
        -String symbol
        -String name
        -double price
        -int quantity
        +updatePrice(newPrice: double): void
    }

    class Market {
        -List<Stock> availableStocks
        +addStock(stock: Stock): void
        +removeStock(stock: Stock): void
        +getStockBySymbol(String symbol): Stock
    }

    class UserView {
        +displayUserInfo(user: User): void
        +displayOwnedStocks(user: User): void
        +displayMarketStocks(market: Market): void
        +displayTransactionResult(message: String): void
    }

    class StockView {
        +displayStockDetails(stock: Stock): void
        +displayStockList(stocks: List<Stock>): void
    }

    class DashboardView {
        -Label userInfoLabel
        -TableView<Stock> ownedStocksTable
        -TableView<Stock> marketStocksTable
        -Button buyButton
        -Button sellButton
        +displayDashboard(user: User, market: Market): void
    }

    class LoginView {
        -TextField usernameField
        -Button loginButton
        +displayLoginScreen(): void
    }

    class UserController {
        -User user
        -Market market
        -UserView userView
        -DashboardView dashboardView
        +buyStock(symbol: String, quantity: int): void
        +sellStock(symbol: String, quantity: int): void
        +showUserProfile(): void
        +showMarketStocks(): void
    }

    class StockController {
        -Market market
        -StockView stockView
        -DashboardView dashboardView
        +updateStockPrice(symbol: String, newPrice: double): void
        +addStockToMarket(stock: Stock): void
        +removeStockFromMarket(symbol: String): void
        +showStockDetails(symbol: String): void
    }

    class MainApp {
        +start(primaryStage: Stage): void
    }

    User "1" --> "1" UserController
    Stock "1" --> "1" Market
    Market "1" --> "many" Stock
    UserController "1" --> "1" UserView
    UserController "1" --> "1" DashboardView
    StockController "1" --> "1" Market
    StockController "1" --> "1" StockView
    StockController "1" --> "1" DashboardView
    MainApp "1" --> "1" UserController
    MainApp "1" --> "1" StockController
    MainApp "1" --> "1" LoginView
    MainApp "1" --> "1" DashboardView
    LoginView "1" --> "1"
