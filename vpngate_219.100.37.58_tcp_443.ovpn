// Định nghĩa các biến đầu vào
extern double Lots = 0.1;
extern double StopLoss = 30;
extern double TakeProfit = 60;
extern int TrailingStop = 0;

// Hàm khởi tạo cho robot
int OnInit()
{
    // Kích hoạt sự kiện OnTick
    EventSetTimer(1);
    return(INIT_SUCCEEDED);
}

// Hàm xử lý sự kiện OnTick
void OnTick()
{
    // Lấy giá trị EMA20 và EMA50
    double ema20 = iMA(_Symbol, PERIOD_M1, 20, 0, MODE_EMA, PRICE_CLOSE, 0);
    double ema50 = iMA(_Symbol, PERIOD_M1, 50, 0, MODE_EMA, PRICE_CLOSE, 0);

    // Lấy giá đóng và giá mở của thanh nến hiện tại
    double closePrice = Close[0];
    double openPrice = Open[0];

    // Kiểm tra điều kiện mua
    if (ema20 < ema50 && closePrice >= ema50 && openPrice <= ema20)
    {
        double sl = Bid - StopLoss * _Point;
        double tp = Bid + TakeProfit * _Point;
        int ticket = OrderSend(_Symbol, OP_BUY, Lots, Ask, 3, sl, tp, "Buy", MagicNumber, 0, Green);
        if (ticket > 0)
        {
            Print("Mở vị thế mua thành công, ticket = ", ticket);
        }
        else
        {
            Print("Mở vị thế mua không thành công, lỗi mã số ", GetLastError());
        }
    }

    // Kiểm tra điều kiện bán
    if (ema20 > ema50 && closePrice <= ema50 && openPrice >= ema20)
    {
        double sl = Ask + StopLoss * _Point;
        double tp = Ask - TakeProfit * _Point;
        int ticket = OrderSend(_Symbol, OP_SELL, Lots, Bid, 3, sl, tp, "Sell", MagicNumber, 0, Red);
        if (ticket > 0)
        {
            Print("Mở vị thế bán thành công, ticket = ", ticket);
        }
        else
        {
            Print("Mở vị thế bán không thành công, lỗi mã số ", GetLastError());
        }
    }
}
