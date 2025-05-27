//@version=6
indicator("Engulfing Reversal - Narendra", shorttitle = "Engulfing Reversal - Narendra", overlay=true)



a1 = true
a2 = true
var a3 = "SMA50"
var a4 = "SMA50, SMA200"
var a5 = input.string(a3, "Detect Trend Based On", options=[a3, a4, "No detection"])

if a5 == a3
    a6 = ta.sma(close, 50)
    a1 := close < a6
    a2 := close > a6

if a5 == a4
    a7 = ta.sma(close, 200)
    a8 = ta.sma(close, 50)
    a1 := close < a8 and a8 < a7
    a2 := close > a8 and a8 > a7

a9 = 14
a10 = 5.0
a11 = 100.0
a12 = 5.0
a13 = 2.0

a14 = math.max(close, open)
a15 = math.min(close, open)
a16 = a14 - a15
a17 = ta.ema(a16, a9)
a18 = a16 < a17
a19 = a16 > a17
a20 = high - a14
a21 = a15 - low
a22 = a20 > a10 / 100 * a16
a23 = a21 > a10 / 100 * a16
a24 = open < close
a25 = open > close
a26 = high - low
a27 = a14[1] > a14 and a15[1] < a15
a28 = a16 / 2 + a15
a29 = a20 == a21 or (math.abs(a20 - a21) / a21 * 100) < a11 and (math.abs(a21 - a20) / a20 * 100) < a11
a30 = a26 > 0 and a16 <= a26 * a12 / 100
a31 = a30 and a29

a32 = low - (ta.atr(30) * 0.6)
a33 = high + (ta.atr(30) * 0.6)

// Updated to a more pleasant teal-blue theme
a34 = input(color.new(color.teal, 0), "Label Color Bullish")

a35 = 2
a36 = a1 and a24 and a19 and a25[1] and a18[1] and close >= open[1] and open <= close[1] and (close > open[1] or open < close[1])

alertcondition(a36, title = "New pattern detected", message = "New Engulfing – Bullish pattern detected")

if a36
    var a37 = "Engulfing\nAt the end of a given downward trend, there will most likely be a reversal pattern. To distinguish the first day, this candlestick pattern uses a small body, followed by a day where the candle body fully overtakes the body from the day before, and closes in the trend’s opposite direction. Although similar to the outside reversal chart pattern, it is not essential for this pattern to completely overtake the range (high to low), rather only the open and the close."
    label.new(bar_index, a32, text="BE", style=label.style_label_up, color=a34, textcolor=color.white, tooltip=a37)

// Softer background using translucent teal
bgcolor(ta.highest(a36 ? 1 : 0, a35) != 0 ? color.new(color.teal, 85) : na, offset=-(a35 - 1))

b1 = true
b2 = true
var b3 = "SMA50"
var b4 = "SMA50, SMA200"
var b5 = input.string(b3, "Detect Trend Based On", options=[b3, b4, "No detection"])

if b5 == b3
    b6 = ta.sma(close, 50)
    b1 := close < b6
    b2 := close > b6

if b5 == b4
    b7 = ta.sma(close, 200)
    b8 = ta.sma(close, 50)
    b1 := close < b8 and b8 < b7
    b2 := close > b8 and b8 > b7

b9 = 14
b10 = 5.0
b11 = 100.0
b12 = 5.0
b13 = 2.0

b14 = math.max(close, open)
b15 = math.min(close, open)
b16 = b14 - b15
b17 = ta.ema(b16, b9)
b18 = b16 < b17
b19 = b16 > b17
b20 = high - b14
b21 = b15 - low
b22 = b20 > b10 / 100 * b16
b23 = b21 > b10 / 100 * b16
b24 = open < close
b25 = open > close
b26 = high - low
b27 = b14[1] > b14 and b15[1] < b15
b28 = b16 / 2 + b15
b29 = b20 == b21 or (math.abs(b20 - b21) / b21 * 100) < b11 and (math.abs(b21 - b20) / b20 * 100) < b11
b30 = b26 > 0 and b16 <= b26 * b12 / 100
b31 = b30 and b29

b32 = low - (ta.atr(30) * 0.6)
b33 = high + (ta.atr(30) * 0.6)

// Use pleasant coral-red for bearish color
b34 = input(color.new(color.rgb(255, 100, 100), 0), "Label Color Bearish")

b35 = 2
b36 = b2 and b25 and b19 and b24[1] and b18[1] and close <= open[1] and open >= close[1] and (close < open[1] or open > close[1])

alertcondition(b36, title = "New pattern detected", message = "New Engulfing – Bearish pattern detected")

if b36
    var b37 = "Engulfing\nAt the end of a given uptrend, a reversal pattern will most likely appear. During the first day, this candlestick pattern uses a small body. It is then followed by a day where the candle body fully overtakes the body from the day before it and closes in the trend’s opposite direction. Although similar to the outside reversal chart pattern, it is not essential for this pattern to fully overtake the range (high to low), rather only the open and the close."
    label.new(bar_index, b33, text="BE", style=label.style_label_down, color=b34, textcolor=color.white, tooltip=b37)

// Soft coral background to highlight pattern gently
bgcolor(ta.highest(b36 ? 1 : 0, b35) != 0 ? color.new(color.rgb(255, 100, 100), 85) : na, offset=-(b35 - 1))

