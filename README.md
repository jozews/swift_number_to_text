# swift_number_to_text
Swift implementation to convert Int into it's String name


func numberToText(_ number: Int) -> String {

    let namesNumber = ["", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve", "thirteen", "fourteen", "fifteen", "sixteen", "seventeen", "eighteen", "nineteen"]
    let namesTenth = ["", "", "twenty", "thirty", "forty", "fifty", "sixty", "seventy", "eighty", "ninety"]
    let namesGroup = ["", "thousand", "million", "billion", "trillion"]

    let digits = Array(String(number)).map { Int(String($0)) }
    let countDigits = digits.count
    let countGroups = Int(Double(countDigits - 1) / 3.0) + 1

    var text = ""
    var textGroup = ""

    for (indexDigit, digit) in digits.enumerated() {
        
        let positionDigit = (countDigits - 1 - indexDigit) % 3
        let digit = digits[indexDigit]!

        if positionDigit == 2 {
            let nameNumber = namesNumber[digit]
            textGroup += " \(nameNumber) hundred"
        }
        else if positionDigit == 1 && digit >= 2 {
            let nameTenth = namesTenth[digit]
            textGroup += " \(nameTenth)"
        }
        else if positionDigit == 0 {
            if indexDigit - 1 >= 0 && digits[indexDigit - 1]! == 1 {
                let numberComposed = digits[indexDigit - 1]! * 10 + digit
                let nameNumber = namesNumber[numberComposed]
                textGroup += " \(nameNumber)"
            }
            else {
                let nameNumber = namesNumber[digit]
                textGroup += " \(nameNumber)"
            }
        }

        if positionDigit == 0 {

            let indexGroup = countGroups - 1 - Int(Double(indexDigit) / 3.0)

            if indexGroup > 0 {
                let nameGroup = namesGroup[indexGroup]
                textGroup += " \(nameGroup)"
            }

            text += textGroup
            textGroup = ""
        }
    }

    text = text.trimmingCharacters(in: .whitespacesAndNewlines)
    return text
}
