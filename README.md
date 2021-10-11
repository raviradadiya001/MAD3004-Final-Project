Student Name&Id 1:Ravi Radadiya  - 0836175
		2.Rohankumar Ghevariya - 0847621

import Foundation
class StockHolding: NSObject {
    var purchaseSharePrice: Float = 0.0
    var currentSharePrice: Float = 0.0
    var numberOfShares: Int = 0
    var companyName: String = ""
    
    init(PSP: Float, CSP: Float, NS: Int, CN: String) {
        purchaseSharePrice = PSP
        currentSharePrice = CSP
        numberOfShares = NS
        companyName = CN
    }
    
    func getPurchaseSharePrice() -> Float {
        return purchaseSharePrice
    }
    
    func getCurrentSharePrice() -> Float {
        return currentSharePrice
    }
    
    func getNumberOfShares() -> Int {
        return numberOfShares
    }
    
    func getCompanyName() -> String {
        return companyName
    }
    
    func costInDollars() -> Float {
        return purchaseSharePrice * Float(numberOfShares)
    }
    
    func valueInDollars() -> Float {
        return currentSharePrice * Float(numberOfShares)
    }
    
    func toString() -> String{
        return "Company Name: \(companyName)\tNumber of Shares: \(numberOfShares)\tShare Purhcase Price: \(purchaseSharePrice)\tShare Current Price: \(currentSharePrice)\nCost in Dollars: \(costInDollars())\tValue in Dollars: \(valueInDollars())"
    }
}

class ForeignStockHolding: StockHolding {
    var conversionRate: Float = 0.0
    
    init(PSP: Float, CSP: Float, NS: Int, CN: String, CR: Float) {
        super.init(PSP: PSP, CSP: CSP, NS: NS, CN: CN)
        conversionRate = CR
    }
    
    override func costInDollars() -> Float {
        return purchaseSharePrice * Float(numberOfShares) * conversionRate
    }
    
    override func valueInDollars() -> Float {
        return currentSharePrice * Float(numberOfShares) * conversionRate
    }
}

//  1st
//  {

func sortArray(stocka: StockHolding, stockb: StockHolding) -> Bool {
    return stocka.getCompanyName() < stockb.getCompanyName()
}

func printStocks(s: StockHolding) {
    print(s.toString())
}
repeat{
var Stocks: Array = [StockHolding(PSP: 2.30, CSP: 4.50, NS: 40, CN: "AB"), StockHolding(PSP: 12.19, CSP: 10.56, NS: 90, CN: "AA"), StockHolding(PSP: 45.10, CSP: 49.51, NS: 210, CN: "C")]
// add more 8 stocks and set some proper company names

Stocks.sort(by: sortArray)

Stocks.forEach(printStocks)
print("\n\n\n")
//  }

//  2nd
//  {
func sortArrayinReverseOrder(stocka: StockHolding, stockb: StockHolding) -> Bool {
    return stocka.getCompanyName() > stockb.getCompanyName()
}

// change company names 
Stocks.append(ForeignStockHolding(PSP: 2.30, CSP: 4.50, NS: 40, CN: "DD", CR: 0.94))
Stocks.append(ForeignStockHolding(PSP: 20.80, CSP: 45.90, NS: 193, CN: "EE", CR: 0.85))

Stocks.sort(by: sortArrayinReverseOrder)

Stocks.forEach(printStocks)
print("\n\n\n")
//  }

//  3rd
//  {

func sortArrayToLowestToHighst(stocka: StockHolding, stockb: StockHolding) -> Bool {
    return stocka.valueInDollars() < stockb.valueInDollars()
}

func sortArrayToHighstToLowest(stocka: StockHolding, stockb: StockHolding) -> Bool {
    return stocka.valueInDollars() > stockb.valueInDollars()
}

func sortArrayToMostProfitable(stocka: StockHolding, stockb: StockHolding) -> Bool {
    return stocka.valueInDollars()-stocka.costInDollars() > stockb.valueInDollars()-stockb.costInDollars()
}

func sortArrayToLessProfitable(stocka: StockHolding, stockb: StockHolding) -> Bool {
    return stocka.valueInDollars()-stocka.costInDollars() < stockb.valueInDollars()-stockb.costInDollars()
}

//append some stokes in  stocks array 

//  1 = Display stock information with the lowest value
//  2 = Display stock with the highest value
//  3 = Display the most profitable stock
//  4 = Display the least profitable stock
//  5 = List all stocks sorted by company name (A-Z)
//  6 = List all stocks sorted from the lowest value to the highest value

//var option:Int = 3
print ("Make your choice from the following Options.\n1 = Display stock information with the lowest value.\n2 = Display stock with the highest value.\n3 = Display the most profitable stock.\n4 = Display the least profitable stock.\n5 = List all stocks sorted by company name (A-Z).\n6 = List all stocks sorted from the lowest value to the highest value.\n7 = Return to Main Menu")
switch (Int(readLine()!)!) {
case 1:
    Stocks.sort(by: sortArrayToLowestToHighst)
    print("Lowest Valuable Stock\n\(Stocks[0].toString())")
case 2:
    Stocks.sort(by: sortArrayToHighstToLowest)
    print("Highst Valuable Stock\n\(Stocks[0].toString())")
case 3:
    Stocks.sort(by: sortArrayToMostProfitable)
    print("Most Profitable Stock\n\(Stocks[0].toString())")
case 4:
    Stocks.sort(by: sortArrayToLessProfitable)
    print("Less Profitable Stock\n\(Stocks[0].toString())")
case 5:
    print("Sorted by company name in A-Z \n")
    Stocks.sort(by: sortArray)
    Stocks.forEach(printStocks)
case 6:
    print("Sorted by Stock Value in low-high \n")
    Stocks.sort(by: sortArrayToLowestToHighst)
    Stocks.forEach(printStocks)

	
default:
    print("please select from 1 to 7") 
}

	print("Do you want to make more choice? yes/no" )
}while(readLine()!.lowercased() == "yes")

//  }



