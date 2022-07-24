# 

```mongo
db.statistics.aggregate([{
    "$match": {
        "date": 1598198400
    }
}, {
    $group: {
        "_id": "$date",
        "Traffic|0000": {
            $sum: "$0000.Traffic"
        },
        "Traffic|0001": {
            $sum: "$0001.Traffic"
        },
        "Traffic|0002": {
            $sum: "$0002.Traffic"
        },
        "Traffic|0003": {
            $sum: "$0003.Traffic"
        },
        "Traffic|0004": {
            $sum: "$0004.Traffic"
        },
        "Traffic|0005": {
            $sum: "$0005.Traffic"
        },
        "Traffic|0006": {
            $sum: "$0006.Traffic"
        },
        "Traffic|0007": {
            $sum: "$0007.Traffic"
        },
        "Traffic|0008": {
            $sum: "$0008.Traffic"
        },
        "Traffic|0009": {
            $sum: "$0009.Traffic"
        },
        "Traffic|0010": {
            $sum: "$0010.Traffic"
        },
        "Traffic|0011": {
            $sum: "$0011.Traffic"
        },
        "Traffic|0012": {
            $sum: "$0012.Traffic"
        },
        "Traffic|0013": {
            $sum: "$0013.Traffic"
        },
        "Traffic|0014": {
            $sum: "$0014.Traffic"
        },
        "Traffic|0015": {
            $sum: "$0015.Traffic"
        },
        "Traffic|0016": {
            $sum: "$0016.Traffic"
        },
        "Traffic|0017": {
            $sum: "$0017.Traffic"
        },
        "Traffic|0018": {
            $sum: "$0018.Traffic"
        },
        "Traffic|0019": {
            $sum: "$0019.Traffic"
        },
        "Traffic|0020": {
            $sum: "$0020.Traffic"
        },
        "Traffic|0021": {
            $sum: "$0021.Traffic"
        },
        "Traffic|0022": {
            $sum: "$0022.Traffic"
        },
        "Traffic|0023": {
            $sum: "$0023.Traffic"
        },
        "Traffic|0024": {
            $sum: "$0024.Traffic"
        },
        "Traffic|0025": {
            $sum: "$0025.Traffic"
        },
        "Traffic|0026": {
            $sum: "$0026.Traffic"
        },
        "Traffic|0027": {
            $sum: "$0027.Traffic"
        },
        "Traffic|0028": {
            $sum: "$0028.Traffic"
        },
        "Traffic|0029": {
            $sum: "$0029.Traffic"
        },
        "Traffic|0030": {
            $sum: "$0030.Traffic"
        },
        "Traffic|0031": {
            $sum: "$0031.Traffic"
        },
        "Traffic|0032": {
            $sum: "$0032.Traffic"
        },
        "Traffic|0033": {
            $sum: "$0033.Traffic"
        },
        "Traffic|0034": {
            $sum: "$0034.Traffic"
        },
        "Traffic|0035": {
            $sum: "$0035.Traffic"
        },
        "Traffic|0036": {
            $sum: "$0036.Traffic"
        },
        "Traffic|0037": {
            $sum: "$0037.Traffic"
        },
        "Traffic|0038": {
            $sum: "$0038.Traffic"
        },
        "Traffic|0039": {
            $sum: "$0039.Traffic"
        },
        "Traffic|0040": {
            $sum: "$0040.Traffic"
        },
        "Traffic|0041": {
            $sum: "$0041.Traffic"
        },
        "Traffic|0042": {
            $sum: "$0042.Traffic"
        },
        "Traffic|0043": {
            $sum: "$0043.Traffic"
        },
        "Traffic|0044": {
            $sum: "$0044.Traffic"
        },
        "Traffic|0045": {
            $sum: "$0045.Traffic"
        },
        "Traffic|0046": {
            $sum: "$0046.Traffic"
        },
        "Traffic|0047": {
            $sum: "$0047.Traffic"
        },
        "Traffic|0048": {
            $sum: "$0048.Traffic"
        },
        "Traffic|0049": {
            $sum: "$0049.Traffic"
        },
        "Traffic|0050": {
            $sum: "$0050.Traffic"
        },
        "Traffic|0051": {
            $sum: "$0051.Traffic"
        },
        "Traffic|0052": {
            $sum: "$0052.Traffic"
        },
        "Traffic|0053": {
            $sum: "$0053.Traffic"
        },
        "Traffic|0054": {
            $sum: "$0054.Traffic"
        },
        "Traffic|0055": {
            $sum: "$0055.Traffic"
        },
        "Traffic|0056": {
            $sum: "$0056.Traffic"
        },
        "Traffic|0057": {
            $sum: "$0057.Traffic"
        },
        "Traffic|0058": {
            $sum: "$0058.Traffic"
        },
        "Traffic|0059": {
            $sum: "$0059.Traffic"
        },
        "Traffic|0100": {
            $sum: "$0100.Traffic"
        },
        "Traffic|0101": {
            $sum: "$0101.Traffic"
        },
        "Traffic|0102": {
            $sum: "$0102.Traffic"
        },
        "Traffic|0103": {
            $sum: "$0103.Traffic"
        },
        "Traffic|0104": {
            $sum: "$0104.Traffic"
        },
        "Traffic|0105": {
            $sum: "$0105.Traffic"
        },
        "Traffic|0106": {
            $sum: "$0106.Traffic"
        },
        "Traffic|0107": {
            $sum: "$0107.Traffic"
        },
        "Traffic|0108": {
            $sum: "$0108.Traffic"
        },
        "Traffic|0109": {
            $sum: "$0109.Traffic"
        },
        "Traffic|0110": {
            $sum: "$0110.Traffic"
        },
        "Traffic|0111": {
            $sum: "$0111.Traffic"
        },
        "Traffic|0112": {
            $sum: "$0112.Traffic"
        },
        "Traffic|0113": {
            $sum: "$0113.Traffic"
        },
        "Traffic|0114": {
            $sum: "$0114.Traffic"
        },
        "Traffic|0115": {
            $sum: "$0115.Traffic"
        },
        "Traffic|0116": {
            $sum: "$0116.Traffic"
        },
        "Traffic|0117": {
            $sum: "$0117.Traffic"
        },
        "Traffic|0118": {
            $sum: "$0118.Traffic"
        },
        "Traffic|0119": {
            $sum: "$0119.Traffic"
        },
        "Traffic|0120": {
            $sum: "$0120.Traffic"
        },
        "Traffic|0121": {
            $sum: "$0121.Traffic"
        },
        "Traffic|0122": {
            $sum: "$0122.Traffic"
        },
        "Traffic|0123": {
            $sum: "$0123.Traffic"
        },
        "Traffic|0124": {
            $sum: "$0124.Traffic"
        },
        "Traffic|0125": {
            $sum: "$0125.Traffic"
        },
        "Traffic|0126": {
            $sum: "$0126.Traffic"
        },
        "Traffic|0127": {
            $sum: "$0127.Traffic"
        },
        "Traffic|0128": {
            $sum: "$0128.Traffic"
        },
        "Traffic|0129": {
            $sum: "$0129.Traffic"
        },
        "Traffic|0130": {
            $sum: "$0130.Traffic"
        },
        "Traffic|0131": {
            $sum: "$0131.Traffic"
        },
        "Traffic|0132": {
            $sum: "$0132.Traffic"
        },
        "Traffic|0133": {
            $sum: "$0133.Traffic"
        },
        "Traffic|0134": {
            $sum: "$0134.Traffic"
        },
        "Traffic|0135": {
            $sum: "$0135.Traffic"
        },
        "Traffic|0136": {
            $sum: "$0136.Traffic"
        },
        "Traffic|0137": {
            $sum: "$0137.Traffic"
        },
        "Traffic|0138": {
            $sum: "$0138.Traffic"
        },
        "Traffic|0139": {
            $sum: "$0139.Traffic"
        },
        "Traffic|0140": {
            $sum: "$0140.Traffic"
        },
        "Traffic|0141": {
            $sum: "$0141.Traffic"
        },
        "Traffic|0142": {
            $sum: "$0142.Traffic"
        },
        "Traffic|0143": {
            $sum: "$0143.Traffic"
        },
        "Traffic|0144": {
            $sum: "$0144.Traffic"
        },
        "Traffic|0145": {
            $sum: "$0145.Traffic"
        },
        "Traffic|0146": {
            $sum: "$0146.Traffic"
        },
        "Traffic|0147": {
            $sum: "$0147.Traffic"
        },
        "Traffic|0148": {
            $sum: "$0148.Traffic"
        },
        "Traffic|0149": {
            $sum: "$0149.Traffic"
        },
        "Traffic|0150": {
            $sum: "$0150.Traffic"
        },
        "Traffic|0151": {
            $sum: "$0151.Traffic"
        },
        "Traffic|0152": {
            $sum: "$0152.Traffic"
        },
        "Traffic|0153": {
            $sum: "$0153.Traffic"
        },
        "Traffic|0154": {
            $sum: "$0154.Traffic"
        },
        "Traffic|0155": {
            $sum: "$0155.Traffic"
        },
        "Traffic|0156": {
            $sum: "$0156.Traffic"
        },
        "Traffic|0157": {
            $sum: "$0157.Traffic"
        },
        "Traffic|0158": {
            $sum: "$0158.Traffic"
        },
        "Traffic|0159": {
            $sum: "$0159.Traffic"
        },
        "Traffic|0200": {
            $sum: "$0200.Traffic"
        },
        "Traffic|0201": {
            $sum: "$0201.Traffic"
        },
        "Traffic|0202": {
            $sum: "$0202.Traffic"
        },
        "Traffic|0203": {
            $sum: "$0203.Traffic"
        },
        "Traffic|0204": {
            $sum: "$0204.Traffic"
        },
        "Traffic|0205": {
            $sum: "$0205.Traffic"
        },
        "Traffic|0206": {
            $sum: "$0206.Traffic"
        },
        "Traffic|0207": {
            $sum: "$0207.Traffic"
        },
        "Traffic|0208": {
            $sum: "$0208.Traffic"
        },
        "Traffic|0209": {
            $sum: "$0209.Traffic"
        },
        "Traffic|0210": {
            $sum: "$0210.Traffic"
        },
        "Traffic|0211": {
            $sum: "$0211.Traffic"
        },
        "Traffic|0212": {
            $sum: "$0212.Traffic"
        },
        "Traffic|0213": {
            $sum: "$0213.Traffic"
        },
        "Traffic|0214": {
            $sum: "$0214.Traffic"
        },
        "Traffic|0215": {
            $sum: "$0215.Traffic"
        },
        "Traffic|0216": {
            $sum: "$0216.Traffic"
        },
        "Traffic|0217": {
            $sum: "$0217.Traffic"
        },
        "Traffic|0218": {
            $sum: "$0218.Traffic"
        },
        "Traffic|0219": {
            $sum: "$0219.Traffic"
        },
        "Traffic|0220": {
            $sum: "$0220.Traffic"
        },
        "Traffic|0221": {
            $sum: "$0221.Traffic"
        },
        "Traffic|0222": {
            $sum: "$0222.Traffic"
        },
        "Traffic|0223": {
            $sum: "$0223.Traffic"
        },
        "Traffic|0224": {
            $sum: "$0224.Traffic"
        },
        "Traffic|0225": {
            $sum: "$0225.Traffic"
        },
        "Traffic|0226": {
            $sum: "$0226.Traffic"
        },
        "Traffic|0227": {
            $sum: "$0227.Traffic"
        },
        "Traffic|0228": {
            $sum: "$0228.Traffic"
        },
        "Traffic|0229": {
            $sum: "$0229.Traffic"
        },
        "Traffic|0230": {
            $sum: "$0230.Traffic"
        },
        "Traffic|0231": {
            $sum: "$0231.Traffic"
        },
        "Traffic|0232": {
            $sum: "$0232.Traffic"
        },
        "Traffic|0233": {
            $sum: "$0233.Traffic"
        },
        "Traffic|0234": {
            $sum: "$0234.Traffic"
        },
        "Traffic|0235": {
            $sum: "$0235.Traffic"
        },
        "Traffic|0236": {
            $sum: "$0236.Traffic"
        },
        "Traffic|0237": {
            $sum: "$0237.Traffic"
        },
        "Traffic|0238": {
            $sum: "$0238.Traffic"
        },
        "Traffic|0239": {
            $sum: "$0239.Traffic"
        },
        "Traffic|0240": {
            $sum: "$0240.Traffic"
        },
        "Traffic|0241": {
            $sum: "$0241.Traffic"
        },
        "Traffic|0242": {
            $sum: "$0242.Traffic"
        },
        "Traffic|0243": {
            $sum: "$0243.Traffic"
        },
        "Traffic|0244": {
            $sum: "$0244.Traffic"
        },
        "Traffic|0245": {
            $sum: "$0245.Traffic"
        },
        "Traffic|0246": {
            $sum: "$0246.Traffic"
        },
        "Traffic|0247": {
            $sum: "$0247.Traffic"
        },
        "Traffic|0248": {
            $sum: "$0248.Traffic"
        },
        "Traffic|0249": {
            $sum: "$0249.Traffic"
        },
        "Traffic|0250": {
            $sum: "$0250.Traffic"
        },
        "Traffic|0251": {
            $sum: "$0251.Traffic"
        },
        "Traffic|0252": {
            $sum: "$0252.Traffic"
        },
        "Traffic|0253": {
            $sum: "$0253.Traffic"
        },
        "Traffic|0254": {
            $sum: "$0254.Traffic"
        },
        "Traffic|0255": {
            $sum: "$0255.Traffic"
        },
        "Traffic|0256": {
            $sum: "$0256.Traffic"
        },
        "Traffic|0257": {
            $sum: "$0257.Traffic"
        },
        "Traffic|0258": {
            $sum: "$0258.Traffic"
        },
        "Traffic|0259": {
            $sum: "$0259.Traffic"
        },
        "Traffic|0300": {
            $sum: "$0300.Traffic"
        },
        "Traffic|0301": {
            $sum: "$0301.Traffic"
        },
        "Traffic|0302": {
            $sum: "$0302.Traffic"
        },
        "Traffic|0303": {
            $sum: "$0303.Traffic"
        },
        "Traffic|0304": {
            $sum: "$0304.Traffic"
        },
        "Traffic|0305": {
            $sum: "$0305.Traffic"
        },
        "Traffic|0306": {
            $sum: "$0306.Traffic"
        },
        "Traffic|0307": {
            $sum: "$0307.Traffic"
        },
        "Traffic|0308": {
            $sum: "$0308.Traffic"
        },
        "Traffic|0309": {
            $sum: "$0309.Traffic"
        },
        "Traffic|0310": {
            $sum: "$0310.Traffic"
        },
        "Traffic|0311": {
            $sum: "$0311.Traffic"
        },
        "Traffic|0312": {
            $sum: "$0312.Traffic"
        },
        "Traffic|0313": {
            $sum: "$0313.Traffic"
        },
        "Traffic|0314": {
            $sum: "$0314.Traffic"
        },
        "Traffic|0315": {
            $sum: "$0315.Traffic"
        },
        "Traffic|0316": {
            $sum: "$0316.Traffic"
        },
        "Traffic|0317": {
            $sum: "$0317.Traffic"
        },
        "Traffic|0318": {
            $sum: "$0318.Traffic"
        },
        "Traffic|0319": {
            $sum: "$0319.Traffic"
        },
        "Traffic|0320": {
            $sum: "$0320.Traffic"
        },
        "Traffic|0321": {
            $sum: "$0321.Traffic"
        },
        "Traffic|0322": {
            $sum: "$0322.Traffic"
        },
        "Traffic|0323": {
            $sum: "$0323.Traffic"
        },
        "Traffic|0324": {
            $sum: "$0324.Traffic"
        },
        "Traffic|0325": {
            $sum: "$0325.Traffic"
        },
        "Traffic|0326": {
            $sum: "$0326.Traffic"
        },
        "Traffic|0327": {
            $sum: "$0327.Traffic"
        },
        "Traffic|0328": {
            $sum: "$0328.Traffic"
        },
        "Traffic|0329": {
            $sum: "$0329.Traffic"
        },
        "Traffic|0330": {
            $sum: "$0330.Traffic"
        },
        "Traffic|0331": {
            $sum: "$0331.Traffic"
        },
        "Traffic|0332": {
            $sum: "$0332.Traffic"
        },
        "Traffic|0333": {
            $sum: "$0333.Traffic"
        },
        "Traffic|0334": {
            $sum: "$0334.Traffic"
        },
        "Traffic|0335": {
            $sum: "$0335.Traffic"
        },
        "Traffic|0336": {
            $sum: "$0336.Traffic"
        },
        "Traffic|0337": {
            $sum: "$0337.Traffic"
        },
        "Traffic|0338": {
            $sum: "$0338.Traffic"
        },
        "Traffic|0339": {
            $sum: "$0339.Traffic"
        },
        "Traffic|0340": {
            $sum: "$0340.Traffic"
        },
        "Traffic|0341": {
            $sum: "$0341.Traffic"
        },
        "Traffic|0342": {
            $sum: "$0342.Traffic"
        },
        "Traffic|0343": {
            $sum: "$0343.Traffic"
        },
        "Traffic|0344": {
            $sum: "$0344.Traffic"
        },
        "Traffic|0345": {
            $sum: "$0345.Traffic"
        },
        "Traffic|0346": {
            $sum: "$0346.Traffic"
        },
        "Traffic|0347": {
            $sum: "$0347.Traffic"
        },
        "Traffic|0348": {
            $sum: "$0348.Traffic"
        },
        "Traffic|0349": {
            $sum: "$0349.Traffic"
        },
        "Traffic|0350": {
            $sum: "$0350.Traffic"
        },
        "Traffic|0351": {
            $sum: "$0351.Traffic"
        },
        "Traffic|0352": {
            $sum: "$0352.Traffic"
        },
        "Traffic|0353": {
            $sum: "$0353.Traffic"
        },
        "Traffic|0354": {
            $sum: "$0354.Traffic"
        },
        "Traffic|0355": {
            $sum: "$0355.Traffic"
        },
        "Traffic|0356": {
            $sum: "$0356.Traffic"
        },
        "Traffic|0357": {
            $sum: "$0357.Traffic"
        },
        "Traffic|0358": {
            $sum: "$0358.Traffic"
        },
        "Traffic|0359": {
            $sum: "$0359.Traffic"
        },
        "Traffic|0400": {
            $sum: "$0400.Traffic"
        },
        "Traffic|0401": {
            $sum: "$0401.Traffic"
        },
        "Traffic|0402": {
            $sum: "$0402.Traffic"
        },
        "Traffic|0403": {
            $sum: "$0403.Traffic"
        },
        "Traffic|0404": {
            $sum: "$0404.Traffic"
        },
        "Traffic|0405": {
            $sum: "$0405.Traffic"
        },
        "Traffic|0406": {
            $sum: "$0406.Traffic"
        },
        "Traffic|0407": {
            $sum: "$0407.Traffic"
        },
        "Traffic|0408": {
            $sum: "$0408.Traffic"
        },
        "Traffic|0409": {
            $sum: "$0409.Traffic"
        },
        "Traffic|0410": {
            $sum: "$0410.Traffic"
        },
        "Traffic|0411": {
            $sum: "$0411.Traffic"
        },
        "Traffic|0412": {
            $sum: "$0412.Traffic"
        },
        "Traffic|0413": {
            $sum: "$0413.Traffic"
        },
        "Traffic|0414": {
            $sum: "$0414.Traffic"
        },
        "Traffic|0415": {
            $sum: "$0415.Traffic"
        },
        "Traffic|0416": {
            $sum: "$0416.Traffic"
        },
        "Traffic|0417": {
            $sum: "$0417.Traffic"
        },
        "Traffic|0418": {
            $sum: "$0418.Traffic"
        },
        "Traffic|0419": {
            $sum: "$0419.Traffic"
        },
        "Traffic|0420": {
            $sum: "$0420.Traffic"
        },
        "Traffic|0421": {
            $sum: "$0421.Traffic"
        },
        "Traffic|0422": {
            $sum: "$0422.Traffic"
        },
        "Traffic|0423": {
            $sum: "$0423.Traffic"
        },
        "Traffic|0424": {
            $sum: "$0424.Traffic"
        },
        "Traffic|0425": {
            $sum: "$0425.Traffic"
        },
        "Traffic|0426": {
            $sum: "$0426.Traffic"
        },
        "Traffic|0427": {
            $sum: "$0427.Traffic"
        },
        "Traffic|0428": {
            $sum: "$0428.Traffic"
        },
        "Traffic|0429": {
            $sum: "$0429.Traffic"
        },
        "Traffic|0430": {
            $sum: "$0430.Traffic"
        },
        "Traffic|0431": {
            $sum: "$0431.Traffic"
        },
        "Traffic|0432": {
            $sum: "$0432.Traffic"
        },
        "Traffic|0433": {
            $sum: "$0433.Traffic"
        },
        "Traffic|0434": {
            $sum: "$0434.Traffic"
        },
        "Traffic|0435": {
            $sum: "$0435.Traffic"
        },
        "Traffic|0436": {
            $sum: "$0436.Traffic"
        },
        "Traffic|0437": {
            $sum: "$0437.Traffic"
        },
        "Traffic|0438": {
            $sum: "$0438.Traffic"
        },
        "Traffic|0439": {
            $sum: "$0439.Traffic"
        },
        "Traffic|0440": {
            $sum: "$0440.Traffic"
        },
        "Traffic|0441": {
            $sum: "$0441.Traffic"
        },
        "Traffic|0442": {
            $sum: "$0442.Traffic"
        },
        "Traffic|0443": {
            $sum: "$0443.Traffic"
        },
        "Traffic|0444": {
            $sum: "$0444.Traffic"
        },
        "Traffic|0445": {
            $sum: "$0445.Traffic"
        },
        "Traffic|0446": {
            $sum: "$0446.Traffic"
        },
        "Traffic|0447": {
            $sum: "$0447.Traffic"
        },
        "Traffic|0448": {
            $sum: "$0448.Traffic"
        },
        "Traffic|0449": {
            $sum: "$0449.Traffic"
        },
        "Traffic|0450": {
            $sum: "$0450.Traffic"
        },
        "Traffic|0451": {
            $sum: "$0451.Traffic"
        },
        "Traffic|0452": {
            $sum: "$0452.Traffic"
        },
        "Traffic|0453": {
            $sum: "$0453.Traffic"
        },
        "Traffic|0454": {
            $sum: "$0454.Traffic"
        },
        "Traffic|0455": {
            $sum: "$0455.Traffic"
        },
        "Traffic|0456": {
            $sum: "$0456.Traffic"
        },
        "Traffic|0457": {
            $sum: "$0457.Traffic"
        },
        "Traffic|0458": {
            $sum: "$0458.Traffic"
        },
        "Traffic|0459": {
            $sum: "$0459.Traffic"
        },
        "Traffic|0500": {
            $sum: "$0500.Traffic"
        },
        "Traffic|0501": {
            $sum: "$0501.Traffic"
        },
        "Traffic|0502": {
            $sum: "$0502.Traffic"
        },
        "Traffic|0503": {
            $sum: "$0503.Traffic"
        },
        "Traffic|0504": {
            $sum: "$0504.Traffic"
        },
        "Traffic|0505": {
            $sum: "$0505.Traffic"
        },
        "Traffic|0506": {
            $sum: "$0506.Traffic"
        },
        "Traffic|0507": {
            $sum: "$0507.Traffic"
        },
        "Traffic|0508": {
            $sum: "$0508.Traffic"
        },
        "Traffic|0509": {
            $sum: "$0509.Traffic"
        },
        "Traffic|0510": {
            $sum: "$0510.Traffic"
        },
        "Traffic|0511": {
            $sum: "$0511.Traffic"
        },
        "Traffic|0512": {
            $sum: "$0512.Traffic"
        },
        "Traffic|0513": {
            $sum: "$0513.Traffic"
        },
        "Traffic|0514": {
            $sum: "$0514.Traffic"
        },
        "Traffic|0515": {
            $sum: "$0515.Traffic"
        },
        "Traffic|0516": {
            $sum: "$0516.Traffic"
        },
        "Traffic|0517": {
            $sum: "$0517.Traffic"
        },
        "Traffic|0518": {
            $sum: "$0518.Traffic"
        },
        "Traffic|0519": {
            $sum: "$0519.Traffic"
        },
        "Traffic|0520": {
            $sum: "$0520.Traffic"
        },
        "Traffic|0521": {
            $sum: "$0521.Traffic"
        },
        "Traffic|0522": {
            $sum: "$0522.Traffic"
        },
        "Traffic|0523": {
            $sum: "$0523.Traffic"
        },
        "Traffic|0524": {
            $sum: "$0524.Traffic"
        },
        "Traffic|0525": {
            $sum: "$0525.Traffic"
        },
        "Traffic|0526": {
            $sum: "$0526.Traffic"
        },
        "Traffic|0527": {
            $sum: "$0527.Traffic"
        },
        "Traffic|0528": {
            $sum: "$0528.Traffic"
        },
        "Traffic|0529": {
            $sum: "$0529.Traffic"
        },
        "Traffic|0530": {
            $sum: "$0530.Traffic"
        },
        "Traffic|0531": {
            $sum: "$0531.Traffic"
        },
        "Traffic|0532": {
            $sum: "$0532.Traffic"
        },
        "Traffic|0533": {
            $sum: "$0533.Traffic"
        },
        "Traffic|0534": {
            $sum: "$0534.Traffic"
        },
        "Traffic|0535": {
            $sum: "$0535.Traffic"
        },
        "Traffic|0536": {
            $sum: "$0536.Traffic"
        },
        "Traffic|0537": {
            $sum: "$0537.Traffic"
        },
        "Traffic|0538": {
            $sum: "$0538.Traffic"
        },
        "Traffic|0539": {
            $sum: "$0539.Traffic"
        },
        "Traffic|0540": {
            $sum: "$0540.Traffic"
        },
        "Traffic|0541": {
            $sum: "$0541.Traffic"
        },
        "Traffic|0542": {
            $sum: "$0542.Traffic"
        },
        "Traffic|0543": {
            $sum: "$0543.Traffic"
        },
        "Traffic|0544": {
            $sum: "$0544.Traffic"
        },
        "Traffic|0545": {
            $sum: "$0545.Traffic"
        },
        "Traffic|0546": {
            $sum: "$0546.Traffic"
        },
        "Traffic|0547": {
            $sum: "$0547.Traffic"
        },
        "Traffic|0548": {
            $sum: "$0548.Traffic"
        },
        "Traffic|0549": {
            $sum: "$0549.Traffic"
        },
        "Traffic|0550": {
            $sum: "$0550.Traffic"
        },
        "Traffic|0551": {
            $sum: "$0551.Traffic"
        },
        "Traffic|0552": {
            $sum: "$0552.Traffic"
        },
        "Traffic|0553": {
            $sum: "$0553.Traffic"
        },
        "Traffic|0554": {
            $sum: "$0554.Traffic"
        },
        "Traffic|0555": {
            $sum: "$0555.Traffic"
        },
        "Traffic|0556": {
            $sum: "$0556.Traffic"
        },
        "Traffic|0557": {
            $sum: "$0557.Traffic"
        },
        "Traffic|0558": {
            $sum: "$0558.Traffic"
        },
        "Traffic|0559": {
            $sum: "$0559.Traffic"
        },
        "Traffic|0600": {
            $sum: "$0600.Traffic"
        },
        "Traffic|0601": {
            $sum: "$0601.Traffic"
        },
        "Traffic|0602": {
            $sum: "$0602.Traffic"
        },
        "Traffic|0603": {
            $sum: "$0603.Traffic"
        },
        "Traffic|0604": {
            $sum: "$0604.Traffic"
        },
        "Traffic|0605": {
            $sum: "$0605.Traffic"
        },
        "Traffic|0606": {
            $sum: "$0606.Traffic"
        },
        "Traffic|0607": {
            $sum: "$0607.Traffic"
        },
        "Traffic|0608": {
            $sum: "$0608.Traffic"
        },
        "Traffic|0609": {
            $sum: "$0609.Traffic"
        },
        "Traffic|0610": {
            $sum: "$0610.Traffic"
        },
        "Traffic|0611": {
            $sum: "$0611.Traffic"
        },
        "Traffic|0612": {
            $sum: "$0612.Traffic"
        },
        "Traffic|0613": {
            $sum: "$0613.Traffic"
        },
        "Traffic|0614": {
            $sum: "$0614.Traffic"
        },
        "Traffic|0615": {
            $sum: "$0615.Traffic"
        },
        "Traffic|0616": {
            $sum: "$0616.Traffic"
        },
        "Traffic|0617": {
            $sum: "$0617.Traffic"
        },
        "Traffic|0618": {
            $sum: "$0618.Traffic"
        },
        "Traffic|0619": {
            $sum: "$0619.Traffic"
        },
        "Traffic|0620": {
            $sum: "$0620.Traffic"
        },
        "Traffic|0621": {
            $sum: "$0621.Traffic"
        },
        "Traffic|0622": {
            $sum: "$0622.Traffic"
        },
        "Traffic|0623": {
            $sum: "$0623.Traffic"
        },
        "Traffic|0624": {
            $sum: "$0624.Traffic"
        },
        "Traffic|0625": {
            $sum: "$0625.Traffic"
        },
        "Traffic|0626": {
            $sum: "$0626.Traffic"
        },
        "Traffic|0627": {
            $sum: "$0627.Traffic"
        },
        "Traffic|0628": {
            $sum: "$0628.Traffic"
        },
        "Traffic|0629": {
            $sum: "$0629.Traffic"
        },
        "Traffic|0630": {
            $sum: "$0630.Traffic"
        },
        "Traffic|0631": {
            $sum: "$0631.Traffic"
        },
        "Traffic|0632": {
            $sum: "$0632.Traffic"
        },
        "Traffic|0633": {
            $sum: "$0633.Traffic"
        },
        "Traffic|0634": {
            $sum: "$0634.Traffic"
        },
        "Traffic|0635": {
            $sum: "$0635.Traffic"
        },
        "Traffic|0636": {
            $sum: "$0636.Traffic"
        },
        "Traffic|0637": {
            $sum: "$0637.Traffic"
        },
        "Traffic|0638": {
            $sum: "$0638.Traffic"
        },
        "Traffic|0639": {
            $sum: "$0639.Traffic"
        },
        "Traffic|0640": {
            $sum: "$0640.Traffic"
        },
        "Traffic|0641": {
            $sum: "$0641.Traffic"
        },
        "Traffic|0642": {
            $sum: "$0642.Traffic"
        },
        "Traffic|0643": {
            $sum: "$0643.Traffic"
        },
        "Traffic|0644": {
            $sum: "$0644.Traffic"
        },
        "Traffic|0645": {
            $sum: "$0645.Traffic"
        },
        "Traffic|0646": {
            $sum: "$0646.Traffic"
        },
        "Traffic|0647": {
            $sum: "$0647.Traffic"
        },
        "Traffic|0648": {
            $sum: "$0648.Traffic"
        },
        "Traffic|0649": {
            $sum: "$0649.Traffic"
        },
        "Traffic|0650": {
            $sum: "$0650.Traffic"
        },
        "Traffic|0651": {
            $sum: "$0651.Traffic"
        },
        "Traffic|0652": {
            $sum: "$0652.Traffic"
        },
        "Traffic|0653": {
            $sum: "$0653.Traffic"
        },
        "Traffic|0654": {
            $sum: "$0654.Traffic"
        },
        "Traffic|0655": {
            $sum: "$0655.Traffic"
        },
        "Traffic|0656": {
            $sum: "$0656.Traffic"
        },
        "Traffic|0657": {
            $sum: "$0657.Traffic"
        },
        "Traffic|0658": {
            $sum: "$0658.Traffic"
        },
        "Traffic|0659": {
            $sum: "$0659.Traffic"
        },
        "Traffic|0700": {
            $sum: "$0700.Traffic"
        },
        "Traffic|0701": {
            $sum: "$0701.Traffic"
        },
        "Traffic|0702": {
            $sum: "$0702.Traffic"
        },
        "Traffic|0703": {
            $sum: "$0703.Traffic"
        },
        "Traffic|0704": {
            $sum: "$0704.Traffic"
        },
        "Traffic|0705": {
            $sum: "$0705.Traffic"
        },
        "Traffic|0706": {
            $sum: "$0706.Traffic"
        },
        "Traffic|0707": {
            $sum: "$0707.Traffic"
        },
        "Traffic|0708": {
            $sum: "$0708.Traffic"
        },
        "Traffic|0709": {
            $sum: "$0709.Traffic"
        },
        "Traffic|0710": {
            $sum: "$0710.Traffic"
        },
        "Traffic|0711": {
            $sum: "$0711.Traffic"
        },
        "Traffic|0712": {
            $sum: "$0712.Traffic"
        },
        "Traffic|0713": {
            $sum: "$0713.Traffic"
        },
        "Traffic|0714": {
            $sum: "$0714.Traffic"
        },
        "Traffic|0715": {
            $sum: "$0715.Traffic"
        },
        "Traffic|0716": {
            $sum: "$0716.Traffic"
        },
        "Traffic|0717": {
            $sum: "$0717.Traffic"
        },
        "Traffic|0718": {
            $sum: "$0718.Traffic"
        },
        "Traffic|0719": {
            $sum: "$0719.Traffic"
        },
        "Traffic|0720": {
            $sum: "$0720.Traffic"
        },
        "Traffic|0721": {
            $sum: "$0721.Traffic"
        },
        "Traffic|0722": {
            $sum: "$0722.Traffic"
        },
        "Traffic|0723": {
            $sum: "$0723.Traffic"
        },
        "Traffic|0724": {
            $sum: "$0724.Traffic"
        },
        "Traffic|0725": {
            $sum: "$0725.Traffic"
        },
        "Traffic|0726": {
            $sum: "$0726.Traffic"
        },
        "Traffic|0727": {
            $sum: "$0727.Traffic"
        },
        "Traffic|0728": {
            $sum: "$0728.Traffic"
        },
        "Traffic|0729": {
            $sum: "$0729.Traffic"
        },
        "Traffic|0730": {
            $sum: "$0730.Traffic"
        },
        "Traffic|0731": {
            $sum: "$0731.Traffic"
        },
        "Traffic|0732": {
            $sum: "$0732.Traffic"
        },
        "Traffic|0733": {
            $sum: "$0733.Traffic"
        },
        "Traffic|0734": {
            $sum: "$0734.Traffic"
        },
        "Traffic|0735": {
            $sum: "$0735.Traffic"
        },
        "Traffic|0736": {
            $sum: "$0736.Traffic"
        },
        "Traffic|0737": {
            $sum: "$0737.Traffic"
        },
        "Traffic|0738": {
            $sum: "$0738.Traffic"
        },
        "Traffic|0739": {
            $sum: "$0739.Traffic"
        },
        "Traffic|0740": {
            $sum: "$0740.Traffic"
        },
        "Traffic|0741": {
            $sum: "$0741.Traffic"
        },
        "Traffic|0742": {
            $sum: "$0742.Traffic"
        },
        "Traffic|0743": {
            $sum: "$0743.Traffic"
        },
        "Traffic|0744": {
            $sum: "$0744.Traffic"
        },
        "Traffic|0745": {
            $sum: "$0745.Traffic"
        },
        "Traffic|0746": {
            $sum: "$0746.Traffic"
        },
        "Traffic|0747": {
            $sum: "$0747.Traffic"
        },
        "Traffic|0748": {
            $sum: "$0748.Traffic"
        },
        "Traffic|0749": {
            $sum: "$0749.Traffic"
        },
        "Traffic|0750": {
            $sum: "$0750.Traffic"
        },
        "Traffic|0751": {
            $sum: "$0751.Traffic"
        },
        "Traffic|0752": {
            $sum: "$0752.Traffic"
        },
        "Traffic|0753": {
            $sum: "$0753.Traffic"
        },
        "Traffic|0754": {
            $sum: "$0754.Traffic"
        },
        "Traffic|0755": {
            $sum: "$0755.Traffic"
        },
        "Traffic|0756": {
            $sum: "$0756.Traffic"
        },
        "Traffic|0757": {
            $sum: "$0757.Traffic"
        },
        "Traffic|0758": {
            $sum: "$0758.Traffic"
        },
        "Traffic|0759": {
            $sum: "$0759.Traffic"
        },
        "Traffic|0800": {
            $sum: "$0800.Traffic"
        },
        "Traffic|0801": {
            $sum: "$0801.Traffic"
        },
        "Traffic|0802": {
            $sum: "$0802.Traffic"
        },
        "Traffic|0803": {
            $sum: "$0803.Traffic"
        },
        "Traffic|0804": {
            $sum: "$0804.Traffic"
        },
        "Traffic|0805": {
            $sum: "$0805.Traffic"
        },
        "Traffic|0806": {
            $sum: "$0806.Traffic"
        },
        "Traffic|0807": {
            $sum: "$0807.Traffic"
        },
        "Traffic|0808": {
            $sum: "$0808.Traffic"
        },
        "Traffic|0809": {
            $sum: "$0809.Traffic"
        },
        "Traffic|0810": {
            $sum: "$0810.Traffic"
        },
        "Traffic|0811": {
            $sum: "$0811.Traffic"
        },
        "Traffic|0812": {
            $sum: "$0812.Traffic"
        },
        "Traffic|0813": {
            $sum: "$0813.Traffic"
        },
        "Traffic|0814": {
            $sum: "$0814.Traffic"
        },
        "Traffic|0815": {
            $sum: "$0815.Traffic"
        },
        "Traffic|0816": {
            $sum: "$0816.Traffic"
        },
        "Traffic|0817": {
            $sum: "$0817.Traffic"
        },
        "Traffic|0818": {
            $sum: "$0818.Traffic"
        },
        "Traffic|0819": {
            $sum: "$0819.Traffic"
        },
        "Traffic|0820": {
            $sum: "$0820.Traffic"
        },
        "Traffic|0821": {
            $sum: "$0821.Traffic"
        },
        "Traffic|0822": {
            $sum: "$0822.Traffic"
        },
        "Traffic|0823": {
            $sum: "$0823.Traffic"
        },
        "Traffic|0824": {
            $sum: "$0824.Traffic"
        },
        "Traffic|0825": {
            $sum: "$0825.Traffic"
        },
        "Traffic|0826": {
            $sum: "$0826.Traffic"
        },
        "Traffic|0827": {
            $sum: "$0827.Traffic"
        },
        "Traffic|0828": {
            $sum: "$0828.Traffic"
        },
        "Traffic|0829": {
            $sum: "$0829.Traffic"
        },
        "Traffic|0830": {
            $sum: "$0830.Traffic"
        },
        "Traffic|0831": {
            $sum: "$0831.Traffic"
        },
        "Traffic|0832": {
            $sum: "$0832.Traffic"
        },
        "Traffic|0833": {
            $sum: "$0833.Traffic"
        },
        "Traffic|0834": {
            $sum: "$0834.Traffic"
        },
        "Traffic|0835": {
            $sum: "$0835.Traffic"
        },
        "Traffic|0836": {
            $sum: "$0836.Traffic"
        },
        "Traffic|0837": {
            $sum: "$0837.Traffic"
        },
        "Traffic|0838": {
            $sum: "$0838.Traffic"
        },
        "Traffic|0839": {
            $sum: "$0839.Traffic"
        },
        "Traffic|0840": {
            $sum: "$0840.Traffic"
        },
        "Traffic|0841": {
            $sum: "$0841.Traffic"
        },
        "Traffic|0842": {
            $sum: "$0842.Traffic"
        },
        "Traffic|0843": {
            $sum: "$0843.Traffic"
        },
        "Traffic|0844": {
            $sum: "$0844.Traffic"
        },
        "Traffic|0845": {
            $sum: "$0845.Traffic"
        },
        "Traffic|0846": {
            $sum: "$0846.Traffic"
        },
        "Traffic|0847": {
            $sum: "$0847.Traffic"
        },
        "Traffic|0848": {
            $sum: "$0848.Traffic"
        },
        "Traffic|0849": {
            $sum: "$0849.Traffic"
        },
        "Traffic|0850": {
            $sum: "$0850.Traffic"
        },
        "Traffic|0851": {
            $sum: "$0851.Traffic"
        },
        "Traffic|0852": {
            $sum: "$0852.Traffic"
        },
        "Traffic|0853": {
            $sum: "$0853.Traffic"
        },
        "Traffic|0854": {
            $sum: "$0854.Traffic"
        },
        "Traffic|0855": {
            $sum: "$0855.Traffic"
        },
        "Traffic|0856": {
            $sum: "$0856.Traffic"
        },
        "Traffic|0857": {
            $sum: "$0857.Traffic"
        },
        "Traffic|0858": {
            $sum: "$0858.Traffic"
        },
        "Traffic|0859": {
            $sum: "$0859.Traffic"
        },
        "Traffic|0900": {
            $sum: "$0900.Traffic"
        },
        "Traffic|0901": {
            $sum: "$0901.Traffic"
        },
        "Traffic|0902": {
            $sum: "$0902.Traffic"
        },
        "Traffic|0903": {
            $sum: "$0903.Traffic"
        },
        "Traffic|0904": {
            $sum: "$0904.Traffic"
        },
        "Traffic|0905": {
            $sum: "$0905.Traffic"
        },
        "Traffic|0906": {
            $sum: "$0906.Traffic"
        },
        "Traffic|0907": {
            $sum: "$0907.Traffic"
        },
        "Traffic|0908": {
            $sum: "$0908.Traffic"
        },
        "Traffic|0909": {
            $sum: "$0909.Traffic"
        },
        "Traffic|0910": {
            $sum: "$0910.Traffic"
        },
        "Traffic|0911": {
            $sum: "$0911.Traffic"
        },
        "Traffic|0912": {
            $sum: "$0912.Traffic"
        },
        "Traffic|0913": {
            $sum: "$0913.Traffic"
        },
        "Traffic|0914": {
            $sum: "$0914.Traffic"
        },
        "Traffic|0915": {
            $sum: "$0915.Traffic"
        },
        "Traffic|0916": {
            $sum: "$0916.Traffic"
        },
        "Traffic|0917": {
            $sum: "$0917.Traffic"
        },
        "Traffic|0918": {
            $sum: "$0918.Traffic"
        },
        "Traffic|0919": {
            $sum: "$0919.Traffic"
        },
        "Traffic|0920": {
            $sum: "$0920.Traffic"
        },
        "Traffic|0921": {
            $sum: "$0921.Traffic"
        },
        "Traffic|0922": {
            $sum: "$0922.Traffic"
        },
        "Traffic|0923": {
            $sum: "$0923.Traffic"
        },
        "Traffic|0924": {
            $sum: "$0924.Traffic"
        },
        "Traffic|0925": {
            $sum: "$0925.Traffic"
        },
        "Traffic|0926": {
            $sum: "$0926.Traffic"
        },
        "Traffic|0927": {
            $sum: "$0927.Traffic"
        },
        "Traffic|0928": {
            $sum: "$0928.Traffic"
        },
        "Traffic|0929": {
            $sum: "$0929.Traffic"
        },
        "Traffic|0930": {
            $sum: "$0930.Traffic"
        },
        "Traffic|0931": {
            $sum: "$0931.Traffic"
        },
        "Traffic|0932": {
            $sum: "$0932.Traffic"
        },
        "Traffic|0933": {
            $sum: "$0933.Traffic"
        },
        "Traffic|0934": {
            $sum: "$0934.Traffic"
        },
        "Traffic|0935": {
            $sum: "$0935.Traffic"
        },
        "Traffic|0936": {
            $sum: "$0936.Traffic"
        },
        "Traffic|0937": {
            $sum: "$0937.Traffic"
        },
        "Traffic|0938": {
            $sum: "$0938.Traffic"
        },
        "Traffic|0939": {
            $sum: "$0939.Traffic"
        },
        "Traffic|0940": {
            $sum: "$0940.Traffic"
        },
        "Traffic|0941": {
            $sum: "$0941.Traffic"
        },
        "Traffic|0942": {
            $sum: "$0942.Traffic"
        },
        "Traffic|0943": {
            $sum: "$0943.Traffic"
        },
        "Traffic|0944": {
            $sum: "$0944.Traffic"
        },
        "Traffic|0945": {
            $sum: "$0945.Traffic"
        },
        "Traffic|0946": {
            $sum: "$0946.Traffic"
        },
        "Traffic|0947": {
            $sum: "$0947.Traffic"
        },
        "Traffic|0948": {
            $sum: "$0948.Traffic"
        },
        "Traffic|0949": {
            $sum: "$0949.Traffic"
        },
        "Traffic|0950": {
            $sum: "$0950.Traffic"
        },
        "Traffic|0951": {
            $sum: "$0951.Traffic"
        },
        "Traffic|0952": {
            $sum: "$0952.Traffic"
        },
        "Traffic|0953": {
            $sum: "$0953.Traffic"
        },
        "Traffic|0954": {
            $sum: "$0954.Traffic"
        },
        "Traffic|0955": {
            $sum: "$0955.Traffic"
        },
        "Traffic|0956": {
            $sum: "$0956.Traffic"
        },
        "Traffic|0957": {
            $sum: "$0957.Traffic"
        },
        "Traffic|0958": {
            $sum: "$0958.Traffic"
        },
        "Traffic|0959": {
            $sum: "$0959.Traffic"
        },
        "Traffic|1000": {
            $sum: "$1000.Traffic"
        },
        "Traffic|1001": {
            $sum: "$1001.Traffic"
        },
        "Traffic|1002": {
            $sum: "$1002.Traffic"
        },
        "Traffic|1003": {
            $sum: "$1003.Traffic"
        },
        "Traffic|1004": {
            $sum: "$1004.Traffic"
        },
        "Traffic|1005": {
            $sum: "$1005.Traffic"
        },
        "Traffic|1006": {
            $sum: "$1006.Traffic"
        },
        "Traffic|1007": {
            $sum: "$1007.Traffic"
        },
        "Traffic|1008": {
            $sum: "$1008.Traffic"
        },
        "Traffic|1009": {
            $sum: "$1009.Traffic"
        },
        "Traffic|1010": {
            $sum: "$1010.Traffic"
        },
        "Traffic|1011": {
            $sum: "$1011.Traffic"
        },
        "Traffic|1012": {
            $sum: "$1012.Traffic"
        },
        "Traffic|1013": {
            $sum: "$1013.Traffic"
        },
        "Traffic|1014": {
            $sum: "$1014.Traffic"
        },
        "Traffic|1015": {
            $sum: "$1015.Traffic"
        },
        "Traffic|1016": {
            $sum: "$1016.Traffic"
        },
        "Traffic|1017": {
            $sum: "$1017.Traffic"
        },
        "Traffic|1018": {
            $sum: "$1018.Traffic"
        },
        "Traffic|1019": {
            $sum: "$1019.Traffic"
        },
        "Traffic|1020": {
            $sum: "$1020.Traffic"
        },
        "Traffic|1021": {
            $sum: "$1021.Traffic"
        },
        "Traffic|1022": {
            $sum: "$1022.Traffic"
        },
        "Traffic|1023": {
            $sum: "$1023.Traffic"
        },
        "Traffic|1024": {
            $sum: "$1024.Traffic"
        },
        "Traffic|1025": {
            $sum: "$1025.Traffic"
        },
        "Traffic|1026": {
            $sum: "$1026.Traffic"
        },
        "Traffic|1027": {
            $sum: "$1027.Traffic"
        },
        "Traffic|1028": {
            $sum: "$1028.Traffic"
        },
        "Traffic|1029": {
            $sum: "$1029.Traffic"
        },
        "Traffic|1030": {
            $sum: "$1030.Traffic"
        },
        "Traffic|1031": {
            $sum: "$1031.Traffic"
        },
        "Traffic|1032": {
            $sum: "$1032.Traffic"
        },
        "Traffic|1033": {
            $sum: "$1033.Traffic"
        },
        "Traffic|1034": {
            $sum: "$1034.Traffic"
        },
        "Traffic|1035": {
            $sum: "$1035.Traffic"
        },
        "Traffic|1036": {
            $sum: "$1036.Traffic"
        },
        "Traffic|1037": {
            $sum: "$1037.Traffic"
        },
        "Traffic|1038": {
            $sum: "$1038.Traffic"
        },
        "Traffic|1039": {
            $sum: "$1039.Traffic"
        },
        "Traffic|1040": {
            $sum: "$1040.Traffic"
        },
        "Traffic|1041": {
            $sum: "$1041.Traffic"
        },
        "Traffic|1042": {
            $sum: "$1042.Traffic"
        },
        "Traffic|1043": {
            $sum: "$1043.Traffic"
        },
        "Traffic|1044": {
            $sum: "$1044.Traffic"
        },
        "Traffic|1045": {
            $sum: "$1045.Traffic"
        },
        "Traffic|1046": {
            $sum: "$1046.Traffic"
        },
        "Traffic|1047": {
            $sum: "$1047.Traffic"
        },
        "Traffic|1048": {
            $sum: "$1048.Traffic"
        },
        "Traffic|1049": {
            $sum: "$1049.Traffic"
        },
        "Traffic|1050": {
            $sum: "$1050.Traffic"
        },
        "Traffic|1051": {
            $sum: "$1051.Traffic"
        },
        "Traffic|1052": {
            $sum: "$1052.Traffic"
        },
        "Traffic|1053": {
            $sum: "$1053.Traffic"
        },
        "Traffic|1054": {
            $sum: "$1054.Traffic"
        },
        "Traffic|1055": {
            $sum: "$1055.Traffic"
        },
        "Traffic|1056": {
            $sum: "$1056.Traffic"
        },
        "Traffic|1057": {
            $sum: "$1057.Traffic"
        },
        "Traffic|1058": {
            $sum: "$1058.Traffic"
        },
        "Traffic|1059": {
            $sum: "$1059.Traffic"
        },
        "Traffic|1100": {
            $sum: "$1100.Traffic"
        },
        "Traffic|1101": {
            $sum: "$1101.Traffic"
        },
        "Traffic|1102": {
            $sum: "$1102.Traffic"
        },
        "Traffic|1103": {
            $sum: "$1103.Traffic"
        },
        "Traffic|1104": {
            $sum: "$1104.Traffic"
        },
        "Traffic|1105": {
            $sum: "$1105.Traffic"
        },
        "Traffic|1106": {
            $sum: "$1106.Traffic"
        },
        "Traffic|1107": {
            $sum: "$1107.Traffic"
        },
        "Traffic|1108": {
            $sum: "$1108.Traffic"
        },
        "Traffic|1109": {
            $sum: "$1109.Traffic"
        },
        "Traffic|1110": {
            $sum: "$1110.Traffic"
        },
        "Traffic|1111": {
            $sum: "$1111.Traffic"
        },
        "Traffic|1112": {
            $sum: "$1112.Traffic"
        },
        "Traffic|1113": {
            $sum: "$1113.Traffic"
        },
        "Traffic|1114": {
            $sum: "$1114.Traffic"
        },
        "Traffic|1115": {
            $sum: "$1115.Traffic"
        },
        "Traffic|1116": {
            $sum: "$1116.Traffic"
        },
        "Traffic|1117": {
            $sum: "$1117.Traffic"
        },
        "Traffic|1118": {
            $sum: "$1118.Traffic"
        },
        "Traffic|1119": {
            $sum: "$1119.Traffic"
        },
        "Traffic|1120": {
            $sum: "$1120.Traffic"
        },
        "Traffic|1121": {
            $sum: "$1121.Traffic"
        },
        "Traffic|1122": {
            $sum: "$1122.Traffic"
        },
        "Traffic|1123": {
            $sum: "$1123.Traffic"
        },
        "Traffic|1124": {
            $sum: "$1124.Traffic"
        },
        "Traffic|1125": {
            $sum: "$1125.Traffic"
        },
        "Traffic|1126": {
            $sum: "$1126.Traffic"
        },
        "Traffic|1127": {
            $sum: "$1127.Traffic"
        },
        "Traffic|1128": {
            $sum: "$1128.Traffic"
        },
        "Traffic|1129": {
            $sum: "$1129.Traffic"
        },
        "Traffic|1130": {
            $sum: "$1130.Traffic"
        },
        "Traffic|1131": {
            $sum: "$1131.Traffic"
        },
        "Traffic|1132": {
            $sum: "$1132.Traffic"
        },
        "Traffic|1133": {
            $sum: "$1133.Traffic"
        },
        "Traffic|1134": {
            $sum: "$1134.Traffic"
        },
        "Traffic|1135": {
            $sum: "$1135.Traffic"
        },
        "Traffic|1136": {
            $sum: "$1136.Traffic"
        },
        "Traffic|1137": {
            $sum: "$1137.Traffic"
        },
        "Traffic|1138": {
            $sum: "$1138.Traffic"
        },
        "Traffic|1139": {
            $sum: "$1139.Traffic"
        },
        "Traffic|1140": {
            $sum: "$1140.Traffic"
        },
        "Traffic|1141": {
            $sum: "$1141.Traffic"
        },
        "Traffic|1142": {
            $sum: "$1142.Traffic"
        },
        "Traffic|1143": {
            $sum: "$1143.Traffic"
        },
        "Traffic|1144": {
            $sum: "$1144.Traffic"
        },
        "Traffic|1145": {
            $sum: "$1145.Traffic"
        },
        "Traffic|1146": {
            $sum: "$1146.Traffic"
        },
        "Traffic|1147": {
            $sum: "$1147.Traffic"
        },
        "Traffic|1148": {
            $sum: "$1148.Traffic"
        },
        "Traffic|1149": {
            $sum: "$1149.Traffic"
        },
        "Traffic|1150": {
            $sum: "$1150.Traffic"
        },
        "Traffic|1151": {
            $sum: "$1151.Traffic"
        },
        "Traffic|1152": {
            $sum: "$1152.Traffic"
        },
        "Traffic|1153": {
            $sum: "$1153.Traffic"
        },
        "Traffic|1154": {
            $sum: "$1154.Traffic"
        },
        "Traffic|1155": {
            $sum: "$1155.Traffic"
        },
        "Traffic|1156": {
            $sum: "$1156.Traffic"
        },
        "Traffic|1157": {
            $sum: "$1157.Traffic"
        },
        "Traffic|1158": {
            $sum: "$1158.Traffic"
        },
        "Traffic|1159": {
            $sum: "$1159.Traffic"
        },
        "Traffic|1200": {
            $sum: "$1200.Traffic"
        },
        "Traffic|1201": {
            $sum: "$1201.Traffic"
        },
        "Traffic|1202": {
            $sum: "$1202.Traffic"
        },
        "Traffic|1203": {
            $sum: "$1203.Traffic"
        },
        "Traffic|1204": {
            $sum: "$1204.Traffic"
        },
        "Traffic|1205": {
            $sum: "$1205.Traffic"
        },
        "Traffic|1206": {
            $sum: "$1206.Traffic"
        },
        "Traffic|1207": {
            $sum: "$1207.Traffic"
        },
        "Traffic|1208": {
            $sum: "$1208.Traffic"
        },
        "Traffic|1209": {
            $sum: "$1209.Traffic"
        },
        "Traffic|1210": {
            $sum: "$1210.Traffic"
        },
        "Traffic|1211": {
            $sum: "$1211.Traffic"
        },
        "Traffic|1212": {
            $sum: "$1212.Traffic"
        },
        "Traffic|1213": {
            $sum: "$1213.Traffic"
        },
        "Traffic|1214": {
            $sum: "$1214.Traffic"
        },
        "Traffic|1215": {
            $sum: "$1215.Traffic"
        },
        "Traffic|1216": {
            $sum: "$1216.Traffic"
        },
        "Traffic|1217": {
            $sum: "$1217.Traffic"
        },
        "Traffic|1218": {
            $sum: "$1218.Traffic"
        },
        "Traffic|1219": {
            $sum: "$1219.Traffic"
        },
        "Traffic|1220": {
            $sum: "$1220.Traffic"
        },
        "Traffic|1221": {
            $sum: "$1221.Traffic"
        },
        "Traffic|1222": {
            $sum: "$1222.Traffic"
        },
        "Traffic|1223": {
            $sum: "$1223.Traffic"
        },
        "Traffic|1224": {
            $sum: "$1224.Traffic"
        },
        "Traffic|1225": {
            $sum: "$1225.Traffic"
        },
        "Traffic|1226": {
            $sum: "$1226.Traffic"
        },
        "Traffic|1227": {
            $sum: "$1227.Traffic"
        },
        "Traffic|1228": {
            $sum: "$1228.Traffic"
        },
        "Traffic|1229": {
            $sum: "$1229.Traffic"
        },
        "Traffic|1230": {
            $sum: "$1230.Traffic"
        },
        "Traffic|1231": {
            $sum: "$1231.Traffic"
        },
        "Traffic|1232": {
            $sum: "$1232.Traffic"
        },
        "Traffic|1233": {
            $sum: "$1233.Traffic"
        },
        "Traffic|1234": {
            $sum: "$1234.Traffic"
        },
        "Traffic|1235": {
            $sum: "$1235.Traffic"
        },
        "Traffic|1236": {
            $sum: "$1236.Traffic"
        },
        "Traffic|1237": {
            $sum: "$1237.Traffic"
        },
        "Traffic|1238": {
            $sum: "$1238.Traffic"
        },
        "Traffic|1239": {
            $sum: "$1239.Traffic"
        },
        "Traffic|1240": {
            $sum: "$1240.Traffic"
        },
        "Traffic|1241": {
            $sum: "$1241.Traffic"
        },
        "Traffic|1242": {
            $sum: "$1242.Traffic"
        },
        "Traffic|1243": {
            $sum: "$1243.Traffic"
        },
        "Traffic|1244": {
            $sum: "$1244.Traffic"
        },
        "Traffic|1245": {
            $sum: "$1245.Traffic"
        },
        "Traffic|1246": {
            $sum: "$1246.Traffic"
        },
        "Traffic|1247": {
            $sum: "$1247.Traffic"
        },
        "Traffic|1248": {
            $sum: "$1248.Traffic"
        },
        "Traffic|1249": {
            $sum: "$1249.Traffic"
        },
        "Traffic|1250": {
            $sum: "$1250.Traffic"
        },
        "Traffic|1251": {
            $sum: "$1251.Traffic"
        },
        "Traffic|1252": {
            $sum: "$1252.Traffic"
        },
        "Traffic|1253": {
            $sum: "$1253.Traffic"
        },
        "Traffic|1254": {
            $sum: "$1254.Traffic"
        },
        "Traffic|1255": {
            $sum: "$1255.Traffic"
        },
        "Traffic|1256": {
            $sum: "$1256.Traffic"
        },
        "Traffic|1257": {
            $sum: "$1257.Traffic"
        },
        "Traffic|1258": {
            $sum: "$1258.Traffic"
        },
        "Traffic|1259": {
            $sum: "$1259.Traffic"
        },
        "Traffic|1300": {
            $sum: "$1300.Traffic"
        },
        "Traffic|1301": {
            $sum: "$1301.Traffic"
        },
        "Traffic|1302": {
            $sum: "$1302.Traffic"
        },
        "Traffic|1303": {
            $sum: "$1303.Traffic"
        },
        "Traffic|1304": {
            $sum: "$1304.Traffic"
        },
        "Traffic|1305": {
            $sum: "$1305.Traffic"
        },
        "Traffic|1306": {
            $sum: "$1306.Traffic"
        },
        "Traffic|1307": {
            $sum: "$1307.Traffic"
        },
        "Traffic|1308": {
            $sum: "$1308.Traffic"
        },
        "Traffic|1309": {
            $sum: "$1309.Traffic"
        },
        "Traffic|1310": {
            $sum: "$1310.Traffic"
        },
        "Traffic|1311": {
            $sum: "$1311.Traffic"
        },
        "Traffic|1312": {
            $sum: "$1312.Traffic"
        },
        "Traffic|1313": {
            $sum: "$1313.Traffic"
        },
        "Traffic|1314": {
            $sum: "$1314.Traffic"
        },
        "Traffic|1315": {
            $sum: "$1315.Traffic"
        },
        "Traffic|1316": {
            $sum: "$1316.Traffic"
        },
        "Traffic|1317": {
            $sum: "$1317.Traffic"
        },
        "Traffic|1318": {
            $sum: "$1318.Traffic"
        },
        "Traffic|1319": {
            $sum: "$1319.Traffic"
        },
        "Traffic|1320": {
            $sum: "$1320.Traffic"
        },
        "Traffic|1321": {
            $sum: "$1321.Traffic"
        },
        "Traffic|1322": {
            $sum: "$1322.Traffic"
        },
        "Traffic|1323": {
            $sum: "$1323.Traffic"
        },
        "Traffic|1324": {
            $sum: "$1324.Traffic"
        },
        "Traffic|1325": {
            $sum: "$1325.Traffic"
        },
        "Traffic|1326": {
            $sum: "$1326.Traffic"
        },
        "Traffic|1327": {
            $sum: "$1327.Traffic"
        },
        "Traffic|1328": {
            $sum: "$1328.Traffic"
        },
        "Traffic|1329": {
            $sum: "$1329.Traffic"
        },
        "Traffic|1330": {
            $sum: "$1330.Traffic"
        },
        "Traffic|1331": {
            $sum: "$1331.Traffic"
        },
        "Traffic|1332": {
            $sum: "$1332.Traffic"
        },
        "Traffic|1333": {
            $sum: "$1333.Traffic"
        },
        "Traffic|1334": {
            $sum: "$1334.Traffic"
        },
        "Traffic|1335": {
            $sum: "$1335.Traffic"
        },
        "Traffic|1336": {
            $sum: "$1336.Traffic"
        },
        "Traffic|1337": {
            $sum: "$1337.Traffic"
        },
        "Traffic|1338": {
            $sum: "$1338.Traffic"
        },
        "Traffic|1339": {
            $sum: "$1339.Traffic"
        },
        "Traffic|1340": {
            $sum: "$1340.Traffic"
        },
        "Traffic|1341": {
            $sum: "$1341.Traffic"
        },
        "Traffic|1342": {
            $sum: "$1342.Traffic"
        },
        "Traffic|1343": {
            $sum: "$1343.Traffic"
        },
        "Traffic|1344": {
            $sum: "$1344.Traffic"
        },
        "Traffic|1345": {
            $sum: "$1345.Traffic"
        },
        "Traffic|1346": {
            $sum: "$1346.Traffic"
        },
        "Traffic|1347": {
            $sum: "$1347.Traffic"
        },
        "Traffic|1348": {
            $sum: "$1348.Traffic"
        },
        "Traffic|1349": {
            $sum: "$1349.Traffic"
        },
        "Traffic|1350": {
            $sum: "$1350.Traffic"
        },
        "Traffic|1351": {
            $sum: "$1351.Traffic"
        },
        "Traffic|1352": {
            $sum: "$1352.Traffic"
        },
        "Traffic|1353": {
            $sum: "$1353.Traffic"
        },
        "Traffic|1354": {
            $sum: "$1354.Traffic"
        },
        "Traffic|1355": {
            $sum: "$1355.Traffic"
        },
        "Traffic|1356": {
            $sum: "$1356.Traffic"
        },
        "Traffic|1357": {
            $sum: "$1357.Traffic"
        },
        "Traffic|1358": {
            $sum: "$1358.Traffic"
        },
        "Traffic|1359": {
            $sum: "$1359.Traffic"
        },
        "Traffic|1400": {
            $sum: "$1400.Traffic"
        },
        "Traffic|1401": {
            $sum: "$1401.Traffic"
        },
        "Traffic|1402": {
            $sum: "$1402.Traffic"
        },
        "Traffic|1403": {
            $sum: "$1403.Traffic"
        },
        "Traffic|1404": {
            $sum: "$1404.Traffic"
        },
        "Traffic|1405": {
            $sum: "$1405.Traffic"
        },
        "Traffic|1406": {
            $sum: "$1406.Traffic"
        },
        "Traffic|1407": {
            $sum: "$1407.Traffic"
        },
        "Traffic|1408": {
            $sum: "$1408.Traffic"
        },
        "Traffic|1409": {
            $sum: "$1409.Traffic"
        },
        "Traffic|1410": {
            $sum: "$1410.Traffic"
        },
        "Traffic|1411": {
            $sum: "$1411.Traffic"
        },
        "Traffic|1412": {
            $sum: "$1412.Traffic"
        },
        "Traffic|1413": {
            $sum: "$1413.Traffic"
        },
        "Traffic|1414": {
            $sum: "$1414.Traffic"
        },
        "Traffic|1415": {
            $sum: "$1415.Traffic"
        },
        "Traffic|1416": {
            $sum: "$1416.Traffic"
        },
        "Traffic|1417": {
            $sum: "$1417.Traffic"
        },
        "Traffic|1418": {
            $sum: "$1418.Traffic"
        },
        "Traffic|1419": {
            $sum: "$1419.Traffic"
        },
        "Traffic|1420": {
            $sum: "$1420.Traffic"
        },
        "Traffic|1421": {
            $sum: "$1421.Traffic"
        },
        "Traffic|1422": {
            $sum: "$1422.Traffic"
        },
        "Traffic|1423": {
            $sum: "$1423.Traffic"
        },
        "Traffic|1424": {
            $sum: "$1424.Traffic"
        },
        "Traffic|1425": {
            $sum: "$1425.Traffic"
        },
        "Traffic|1426": {
            $sum: "$1426.Traffic"
        },
        "Traffic|1427": {
            $sum: "$1427.Traffic"
        },
        "Traffic|1428": {
            $sum: "$1428.Traffic"
        },
        "Traffic|1429": {
            $sum: "$1429.Traffic"
        },
        "Traffic|1430": {
            $sum: "$1430.Traffic"
        },
        "Traffic|1431": {
            $sum: "$1431.Traffic"
        },
        "Traffic|1432": {
            $sum: "$1432.Traffic"
        },
        "Traffic|1433": {
            $sum: "$1433.Traffic"
        },
        "Traffic|1434": {
            $sum: "$1434.Traffic"
        },
        "Traffic|1435": {
            $sum: "$1435.Traffic"
        },
        "Traffic|1436": {
            $sum: "$1436.Traffic"
        },
        "Traffic|1437": {
            $sum: "$1437.Traffic"
        },
        "Traffic|1438": {
            $sum: "$1438.Traffic"
        },
        "Traffic|1439": {
            $sum: "$1439.Traffic"
        },
        "Traffic|1440": {
            $sum: "$1440.Traffic"
        },
        "Traffic|1441": {
            $sum: "$1441.Traffic"
        },
        "Traffic|1442": {
            $sum: "$1442.Traffic"
        },
        "Traffic|1443": {
            $sum: "$1443.Traffic"
        },
        "Traffic|1444": {
            $sum: "$1444.Traffic"
        },
        "Traffic|1445": {
            $sum: "$1445.Traffic"
        },
        "Traffic|1446": {
            $sum: "$1446.Traffic"
        },
        "Traffic|1447": {
            $sum: "$1447.Traffic"
        },
        "Traffic|1448": {
            $sum: "$1448.Traffic"
        },
        "Traffic|1449": {
            $sum: "$1449.Traffic"
        },
        "Traffic|1450": {
            $sum: "$1450.Traffic"
        },
        "Traffic|1451": {
            $sum: "$1451.Traffic"
        },
        "Traffic|1452": {
            $sum: "$1452.Traffic"
        },
        "Traffic|1453": {
            $sum: "$1453.Traffic"
        },
        "Traffic|1454": {
            $sum: "$1454.Traffic"
        },
        "Traffic|1455": {
            $sum: "$1455.Traffic"
        },
        "Traffic|1456": {
            $sum: "$1456.Traffic"
        },
        "Traffic|1457": {
            $sum: "$1457.Traffic"
        },
        "Traffic|1458": {
            $sum: "$1458.Traffic"
        },
        "Traffic|1459": {
            $sum: "$1459.Traffic"
        },
        "Traffic|1500": {
            $sum: "$1500.Traffic"
        },
        "Traffic|1501": {
            $sum: "$1501.Traffic"
        },
        "Traffic|1502": {
            $sum: "$1502.Traffic"
        },
        "Traffic|1503": {
            $sum: "$1503.Traffic"
        },
        "Traffic|1504": {
            $sum: "$1504.Traffic"
        },
        "Traffic|1505": {
            $sum: "$1505.Traffic"
        },
        "Traffic|1506": {
            $sum: "$1506.Traffic"
        },
        "Traffic|1507": {
            $sum: "$1507.Traffic"
        },
        "Traffic|1508": {
            $sum: "$1508.Traffic"
        },
        "Traffic|1509": {
            $sum: "$1509.Traffic"
        },
        "Traffic|1510": {
            $sum: "$1510.Traffic"
        },
        "Traffic|1511": {
            $sum: "$1511.Traffic"
        },
        "Traffic|1512": {
            $sum: "$1512.Traffic"
        },
        "Traffic|1513": {
            $sum: "$1513.Traffic"
        },
        "Traffic|1514": {
            $sum: "$1514.Traffic"
        },
        "Traffic|1515": {
            $sum: "$1515.Traffic"
        },
        "Traffic|1516": {
            $sum: "$1516.Traffic"
        },
        "Traffic|1517": {
            $sum: "$1517.Traffic"
        },
        "Traffic|1518": {
            $sum: "$1518.Traffic"
        },
        "Traffic|1519": {
            $sum: "$1519.Traffic"
        },
        "Traffic|1520": {
            $sum: "$1520.Traffic"
        },
        "Traffic|1521": {
            $sum: "$1521.Traffic"
        },
        "Traffic|1522": {
            $sum: "$1522.Traffic"
        },
        "Traffic|1523": {
            $sum: "$1523.Traffic"
        },
        "Traffic|1524": {
            $sum: "$1524.Traffic"
        },
        "Traffic|1525": {
            $sum: "$1525.Traffic"
        },
        "Traffic|1526": {
            $sum: "$1526.Traffic"
        },
        "Traffic|1527": {
            $sum: "$1527.Traffic"
        },
        "Traffic|1528": {
            $sum: "$1528.Traffic"
        },
        "Traffic|1529": {
            $sum: "$1529.Traffic"
        },
        "Traffic|1530": {
            $sum: "$1530.Traffic"
        },
        "Traffic|1531": {
            $sum: "$1531.Traffic"
        },
        "Traffic|1532": {
            $sum: "$1532.Traffic"
        },
        "Traffic|1533": {
            $sum: "$1533.Traffic"
        },
        "Traffic|1534": {
            $sum: "$1534.Traffic"
        },
        "Traffic|1535": {
            $sum: "$1535.Traffic"
        },
        "Traffic|1536": {
            $sum: "$1536.Traffic"
        },
        "Traffic|1537": {
            $sum: "$1537.Traffic"
        },
        "Traffic|1538": {
            $sum: "$1538.Traffic"
        },
        "Traffic|1539": {
            $sum: "$1539.Traffic"
        },
        "Traffic|1540": {
            $sum: "$1540.Traffic"
        },
        "Traffic|1541": {
            $sum: "$1541.Traffic"
        },
        "Traffic|1542": {
            $sum: "$1542.Traffic"
        },
        "Traffic|1543": {
            $sum: "$1543.Traffic"
        },
        "Traffic|1544": {
            $sum: "$1544.Traffic"
        },
        "Traffic|1545": {
            $sum: "$1545.Traffic"
        },
        "Traffic|1546": {
            $sum: "$1546.Traffic"
        },
        "Traffic|1547": {
            $sum: "$1547.Traffic"
        },
        "Traffic|1548": {
            $sum: "$1548.Traffic"
        },
        "Traffic|1549": {
            $sum: "$1549.Traffic"
        },
        "Traffic|1550": {
            $sum: "$1550.Traffic"
        },
        "Traffic|1551": {
            $sum: "$1551.Traffic"
        },
        "Traffic|1552": {
            $sum: "$1552.Traffic"
        },
        "Traffic|1553": {
            $sum: "$1553.Traffic"
        },
        "Traffic|1554": {
            $sum: "$1554.Traffic"
        },
        "Traffic|1555": {
            $sum: "$1555.Traffic"
        },
        "Traffic|1556": {
            $sum: "$1556.Traffic"
        },
        "Traffic|1557": {
            $sum: "$1557.Traffic"
        },
        "Traffic|1558": {
            $sum: "$1558.Traffic"
        },
        "Traffic|1559": {
            $sum: "$1559.Traffic"
        },
        "Traffic|1600": {
            $sum: "$1600.Traffic"
        },
        "Traffic|1601": {
            $sum: "$1601.Traffic"
        },
        "Traffic|1602": {
            $sum: "$1602.Traffic"
        },
        "Traffic|1603": {
            $sum: "$1603.Traffic"
        },
        "Traffic|1604": {
            $sum: "$1604.Traffic"
        },
        "Traffic|1605": {
            $sum: "$1605.Traffic"
        },
        "Traffic|1606": {
            $sum: "$1606.Traffic"
        },
        "Traffic|1607": {
            $sum: "$1607.Traffic"
        },
        "Traffic|1608": {
            $sum: "$1608.Traffic"
        },
        "Traffic|1609": {
            $sum: "$1609.Traffic"
        },
        "Traffic|1610": {
            $sum: "$1610.Traffic"
        },
        "Traffic|1611": {
            $sum: "$1611.Traffic"
        },
        "Traffic|1612": {
            $sum: "$1612.Traffic"
        },
        "Traffic|1613": {
            $sum: "$1613.Traffic"
        },
        "Traffic|1614": {
            $sum: "$1614.Traffic"
        },
        "Traffic|1615": {
            $sum: "$1615.Traffic"
        },
        "Traffic|1616": {
            $sum: "$1616.Traffic"
        },
        "Traffic|1617": {
            $sum: "$1617.Traffic"
        },
        "Traffic|1618": {
            $sum: "$1618.Traffic"
        },
        "Traffic|1619": {
            $sum: "$1619.Traffic"
        },
        "Traffic|1620": {
            $sum: "$1620.Traffic"
        },
        "Traffic|1621": {
            $sum: "$1621.Traffic"
        },
        "Traffic|1622": {
            $sum: "$1622.Traffic"
        },
        "Traffic|1623": {
            $sum: "$1623.Traffic"
        },
        "Traffic|1624": {
            $sum: "$1624.Traffic"
        },
        "Traffic|1625": {
            $sum: "$1625.Traffic"
        },
        "Traffic|1626": {
            $sum: "$1626.Traffic"
        },
        "Traffic|1627": {
            $sum: "$1627.Traffic"
        },
        "Traffic|1628": {
            $sum: "$1628.Traffic"
        },
        "Traffic|1629": {
            $sum: "$1629.Traffic"
        },
        "Traffic|1630": {
            $sum: "$1630.Traffic"
        },
        "Traffic|1631": {
            $sum: "$1631.Traffic"
        },
        "Traffic|1632": {
            $sum: "$1632.Traffic"
        },
        "Traffic|1633": {
            $sum: "$1633.Traffic"
        },
        "Traffic|1634": {
            $sum: "$1634.Traffic"
        },
        "Traffic|1635": {
            $sum: "$1635.Traffic"
        },
        "Traffic|1636": {
            $sum: "$1636.Traffic"
        },
        "Traffic|1637": {
            $sum: "$1637.Traffic"
        },
        "Traffic|1638": {
            $sum: "$1638.Traffic"
        },
        "Traffic|1639": {
            $sum: "$1639.Traffic"
        },
        "Traffic|1640": {
            $sum: "$1640.Traffic"
        },
        "Traffic|1641": {
            $sum: "$1641.Traffic"
        },
        "Traffic|1642": {
            $sum: "$1642.Traffic"
        },
        "Traffic|1643": {
            $sum: "$1643.Traffic"
        },
        "Traffic|1644": {
            $sum: "$1644.Traffic"
        },
        "Traffic|1645": {
            $sum: "$1645.Traffic"
        },
        "Traffic|1646": {
            $sum: "$1646.Traffic"
        },
        "Traffic|1647": {
            $sum: "$1647.Traffic"
        },
        "Traffic|1648": {
            $sum: "$1648.Traffic"
        },
        "Traffic|1649": {
            $sum: "$1649.Traffic"
        },
        "Traffic|1650": {
            $sum: "$1650.Traffic"
        },
        "Traffic|1651": {
            $sum: "$1651.Traffic"
        },
        "Traffic|1652": {
            $sum: "$1652.Traffic"
        },
        "Traffic|1653": {
            $sum: "$1653.Traffic"
        },
        "Traffic|1654": {
            $sum: "$1654.Traffic"
        },
        "Traffic|1655": {
            $sum: "$1655.Traffic"
        },
        "Traffic|1656": {
            $sum: "$1656.Traffic"
        },
        "Traffic|1657": {
            $sum: "$1657.Traffic"
        },
        "Traffic|1658": {
            $sum: "$1658.Traffic"
        },
        "Traffic|1659": {
            $sum: "$1659.Traffic"
        },
        "Traffic|1700": {
            $sum: "$1700.Traffic"
        },
        "Traffic|1701": {
            $sum: "$1701.Traffic"
        },
        "Traffic|1702": {
            $sum: "$1702.Traffic"
        },
        "Traffic|1703": {
            $sum: "$1703.Traffic"
        },
        "Traffic|1704": {
            $sum: "$1704.Traffic"
        },
        "Traffic|1705": {
            $sum: "$1705.Traffic"
        },
        "Traffic|1706": {
            $sum: "$1706.Traffic"
        },
        "Traffic|1707": {
            $sum: "$1707.Traffic"
        },
        "Traffic|1708": {
            $sum: "$1708.Traffic"
        },
        "Traffic|1709": {
            $sum: "$1709.Traffic"
        },
        "Traffic|1710": {
            $sum: "$1710.Traffic"
        },
        "Traffic|1711": {
            $sum: "$1711.Traffic"
        },
        "Traffic|1712": {
            $sum: "$1712.Traffic"
        },
        "Traffic|1713": {
            $sum: "$1713.Traffic"
        },
        "Traffic|1714": {
            $sum: "$1714.Traffic"
        },
        "Traffic|1715": {
            $sum: "$1715.Traffic"
        },
        "Traffic|1716": {
            $sum: "$1716.Traffic"
        },
        "Traffic|1717": {
            $sum: "$1717.Traffic"
        },
        "Traffic|1718": {
            $sum: "$1718.Traffic"
        },
        "Traffic|1719": {
            $sum: "$1719.Traffic"
        },
        "Traffic|1720": {
            $sum: "$1720.Traffic"
        },
        "Traffic|1721": {
            $sum: "$1721.Traffic"
        },
        "Traffic|1722": {
            $sum: "$1722.Traffic"
        },
        "Traffic|1723": {
            $sum: "$1723.Traffic"
        },
        "Traffic|1724": {
            $sum: "$1724.Traffic"
        },
        "Traffic|1725": {
            $sum: "$1725.Traffic"
        },
        "Traffic|1726": {
            $sum: "$1726.Traffic"
        },
        "Traffic|1727": {
            $sum: "$1727.Traffic"
        },
        "Traffic|1728": {
            $sum: "$1728.Traffic"
        },
        "Traffic|1729": {
            $sum: "$1729.Traffic"
        },
        "Traffic|1730": {
            $sum: "$1730.Traffic"
        },
        "Traffic|1731": {
            $sum: "$1731.Traffic"
        },
        "Traffic|1732": {
            $sum: "$1732.Traffic"
        },
        "Traffic|1733": {
            $sum: "$1733.Traffic"
        },
        "Traffic|1734": {
            $sum: "$1734.Traffic"
        },
        "Traffic|1735": {
            $sum: "$1735.Traffic"
        },
        "Traffic|1736": {
            $sum: "$1736.Traffic"
        },
        "Traffic|1737": {
            $sum: "$1737.Traffic"
        },
        "Traffic|1738": {
            $sum: "$1738.Traffic"
        },
        "Traffic|1739": {
            $sum: "$1739.Traffic"
        },
        "Traffic|1740": {
            $sum: "$1740.Traffic"
        },
        "Traffic|1741": {
            $sum: "$1741.Traffic"
        },
        "Traffic|1742": {
            $sum: "$1742.Traffic"
        },
        "Traffic|1743": {
            $sum: "$1743.Traffic"
        },
        "Traffic|1744": {
            $sum: "$1744.Traffic"
        },
        "Traffic|1745": {
            $sum: "$1745.Traffic"
        },
        "Traffic|1746": {
            $sum: "$1746.Traffic"
        },
        "Traffic|1747": {
            $sum: "$1747.Traffic"
        },
        "Traffic|1748": {
            $sum: "$1748.Traffic"
        },
        "Traffic|1749": {
            $sum: "$1749.Traffic"
        },
        "Traffic|1750": {
            $sum: "$1750.Traffic"
        },
        "Traffic|1751": {
            $sum: "$1751.Traffic"
        },
        "Traffic|1752": {
            $sum: "$1752.Traffic"
        },
        "Traffic|1753": {
            $sum: "$1753.Traffic"
        },
        "Traffic|1754": {
            $sum: "$1754.Traffic"
        },
        "Traffic|1755": {
            $sum: "$1755.Traffic"
        },
        "Traffic|1756": {
            $sum: "$1756.Traffic"
        },
        "Traffic|1757": {
            $sum: "$1757.Traffic"
        },
        "Traffic|1758": {
            $sum: "$1758.Traffic"
        },
        "Traffic|1759": {
            $sum: "$1759.Traffic"
        },
        "Traffic|1800": {
            $sum: "$1800.Traffic"
        },
        "Traffic|1801": {
            $sum: "$1801.Traffic"
        },
        "Traffic|1802": {
            $sum: "$1802.Traffic"
        },
        "Traffic|1803": {
            $sum: "$1803.Traffic"
        },
        "Traffic|1804": {
            $sum: "$1804.Traffic"
        },
        "Traffic|1805": {
            $sum: "$1805.Traffic"
        },
        "Traffic|1806": {
            $sum: "$1806.Traffic"
        },
        "Traffic|1807": {
            $sum: "$1807.Traffic"
        },
        "Traffic|1808": {
            $sum: "$1808.Traffic"
        },
        "Traffic|1809": {
            $sum: "$1809.Traffic"
        },
        "Traffic|1810": {
            $sum: "$1810.Traffic"
        },
        "Traffic|1811": {
            $sum: "$1811.Traffic"
        },
        "Traffic|1812": {
            $sum: "$1812.Traffic"
        },
        "Traffic|1813": {
            $sum: "$1813.Traffic"
        },
        "Traffic|1814": {
            $sum: "$1814.Traffic"
        },
        "Traffic|1815": {
            $sum: "$1815.Traffic"
        },
        "Traffic|1816": {
            $sum: "$1816.Traffic"
        },
        "Traffic|1817": {
            $sum: "$1817.Traffic"
        },
        "Traffic|1818": {
            $sum: "$1818.Traffic"
        },
        "Traffic|1819": {
            $sum: "$1819.Traffic"
        },
        "Traffic|1820": {
            $sum: "$1820.Traffic"
        },
        "Traffic|1821": {
            $sum: "$1821.Traffic"
        },
        "Traffic|1822": {
            $sum: "$1822.Traffic"
        },
        "Traffic|1823": {
            $sum: "$1823.Traffic"
        },
        "Traffic|1824": {
            $sum: "$1824.Traffic"
        },
        "Traffic|1825": {
            $sum: "$1825.Traffic"
        },
        "Traffic|1826": {
            $sum: "$1826.Traffic"
        },
        "Traffic|1827": {
            $sum: "$1827.Traffic"
        },
        "Traffic|1828": {
            $sum: "$1828.Traffic"
        },
        "Traffic|1829": {
            $sum: "$1829.Traffic"
        },
        "Traffic|1830": {
            $sum: "$1830.Traffic"
        },
        "Traffic|1831": {
            $sum: "$1831.Traffic"
        },
        "Traffic|1832": {
            $sum: "$1832.Traffic"
        },
        "Traffic|1833": {
            $sum: "$1833.Traffic"
        },
        "Traffic|1834": {
            $sum: "$1834.Traffic"
        },
        "Traffic|1835": {
            $sum: "$1835.Traffic"
        },
        "Traffic|1836": {
            $sum: "$1836.Traffic"
        },
        "Traffic|1837": {
            $sum: "$1837.Traffic"
        },
        "Traffic|1838": {
            $sum: "$1838.Traffic"
        },
        "Traffic|1839": {
            $sum: "$1839.Traffic"
        },
        "Traffic|1840": {
            $sum: "$1840.Traffic"
        },
        "Traffic|1841": {
            $sum: "$1841.Traffic"
        },
        "Traffic|1842": {
            $sum: "$1842.Traffic"
        },
        "Traffic|1843": {
            $sum: "$1843.Traffic"
        },
        "Traffic|1844": {
            $sum: "$1844.Traffic"
        },
        "Traffic|1845": {
            $sum: "$1845.Traffic"
        },
        "Traffic|1846": {
            $sum: "$1846.Traffic"
        },
        "Traffic|1847": {
            $sum: "$1847.Traffic"
        },
        "Traffic|1848": {
            $sum: "$1848.Traffic"
        },
        "Traffic|1849": {
            $sum: "$1849.Traffic"
        },
        "Traffic|1850": {
            $sum: "$1850.Traffic"
        },
        "Traffic|1851": {
            $sum: "$1851.Traffic"
        },
        "Traffic|1852": {
            $sum: "$1852.Traffic"
        },
        "Traffic|1853": {
            $sum: "$1853.Traffic"
        },
        "Traffic|1854": {
            $sum: "$1854.Traffic"
        },
        "Traffic|1855": {
            $sum: "$1855.Traffic"
        },
        "Traffic|1856": {
            $sum: "$1856.Traffic"
        },
        "Traffic|1857": {
            $sum: "$1857.Traffic"
        },
        "Traffic|1858": {
            $sum: "$1858.Traffic"
        },
        "Traffic|1859": {
            $sum: "$1859.Traffic"
        },
        "Traffic|1900": {
            $sum: "$1900.Traffic"
        },
        "Traffic|1901": {
            $sum: "$1901.Traffic"
        },
        "Traffic|1902": {
            $sum: "$1902.Traffic"
        },
        "Traffic|1903": {
            $sum: "$1903.Traffic"
        },
        "Traffic|1904": {
            $sum: "$1904.Traffic"
        },
        "Traffic|1905": {
            $sum: "$1905.Traffic"
        },
        "Traffic|1906": {
            $sum: "$1906.Traffic"
        },
        "Traffic|1907": {
            $sum: "$1907.Traffic"
        },
        "Traffic|1908": {
            $sum: "$1908.Traffic"
        },
        "Traffic|1909": {
            $sum: "$1909.Traffic"
        },
        "Traffic|1910": {
            $sum: "$1910.Traffic"
        },
        "Traffic|1911": {
            $sum: "$1911.Traffic"
        },
        "Traffic|1912": {
            $sum: "$1912.Traffic"
        },
        "Traffic|1913": {
            $sum: "$1913.Traffic"
        },
        "Traffic|1914": {
            $sum: "$1914.Traffic"
        },
        "Traffic|1915": {
            $sum: "$1915.Traffic"
        },
        "Traffic|1916": {
            $sum: "$1916.Traffic"
        },
        "Traffic|1917": {
            $sum: "$1917.Traffic"
        },
        "Traffic|1918": {
            $sum: "$1918.Traffic"
        },
        "Traffic|1919": {
            $sum: "$1919.Traffic"
        },
        "Traffic|1920": {
            $sum: "$1920.Traffic"
        },
        "Traffic|1921": {
            $sum: "$1921.Traffic"
        },
        "Traffic|1922": {
            $sum: "$1922.Traffic"
        },
        "Traffic|1923": {
            $sum: "$1923.Traffic"
        },
        "Traffic|1924": {
            $sum: "$1924.Traffic"
        },
        "Traffic|1925": {
            $sum: "$1925.Traffic"
        },
        "Traffic|1926": {
            $sum: "$1926.Traffic"
        },
        "Traffic|1927": {
            $sum: "$1927.Traffic"
        },
        "Traffic|1928": {
            $sum: "$1928.Traffic"
        },
        "Traffic|1929": {
            $sum: "$1929.Traffic"
        },
        "Traffic|1930": {
            $sum: "$1930.Traffic"
        },
        "Traffic|1931": {
            $sum: "$1931.Traffic"
        },
        "Traffic|1932": {
            $sum: "$1932.Traffic"
        },
        "Traffic|1933": {
            $sum: "$1933.Traffic"
        },
        "Traffic|1934": {
            $sum: "$1934.Traffic"
        },
        "Traffic|1935": {
            $sum: "$1935.Traffic"
        },
        "Traffic|1936": {
            $sum: "$1936.Traffic"
        },
        "Traffic|1937": {
            $sum: "$1937.Traffic"
        },
        "Traffic|1938": {
            $sum: "$1938.Traffic"
        },
        "Traffic|1939": {
            $sum: "$1939.Traffic"
        },
        "Traffic|1940": {
            $sum: "$1940.Traffic"
        },
        "Traffic|1941": {
            $sum: "$1941.Traffic"
        },
        "Traffic|1942": {
            $sum: "$1942.Traffic"
        },
        "Traffic|1943": {
            $sum: "$1943.Traffic"
        },
        "Traffic|1944": {
            $sum: "$1944.Traffic"
        },
        "Traffic|1945": {
            $sum: "$1945.Traffic"
        },
        "Traffic|1946": {
            $sum: "$1946.Traffic"
        },
        "Traffic|1947": {
            $sum: "$1947.Traffic"
        },
        "Traffic|1948": {
            $sum: "$1948.Traffic"
        },
        "Traffic|1949": {
            $sum: "$1949.Traffic"
        },
        "Traffic|1950": {
            $sum: "$1950.Traffic"
        },
        "Traffic|1951": {
            $sum: "$1951.Traffic"
        },
        "Traffic|1952": {
            $sum: "$1952.Traffic"
        },
        "Traffic|1953": {
            $sum: "$1953.Traffic"
        },
        "Traffic|1954": {
            $sum: "$1954.Traffic"
        },
        "Traffic|1955": {
            $sum: "$1955.Traffic"
        },
        "Traffic|1956": {
            $sum: "$1956.Traffic"
        },
        "Traffic|1957": {
            $sum: "$1957.Traffic"
        },
        "Traffic|1958": {
            $sum: "$1958.Traffic"
        },
        "Traffic|1959": {
            $sum: "$1959.Traffic"
        },
        "Traffic|2000": {
            $sum: "$2000.Traffic"
        },
        "Traffic|2001": {
            $sum: "$2001.Traffic"
        },
        "Traffic|2002": {
            $sum: "$2002.Traffic"
        },
        "Traffic|2003": {
            $sum: "$2003.Traffic"
        },
        "Traffic|2004": {
            $sum: "$2004.Traffic"
        },
        "Traffic|2005": {
            $sum: "$2005.Traffic"
        },
        "Traffic|2006": {
            $sum: "$2006.Traffic"
        },
        "Traffic|2007": {
            $sum: "$2007.Traffic"
        },
        "Traffic|2008": {
            $sum: "$2008.Traffic"
        },
        "Traffic|2009": {
            $sum: "$2009.Traffic"
        },
        "Traffic|2010": {
            $sum: "$2010.Traffic"
        },
        "Traffic|2011": {
            $sum: "$2011.Traffic"
        },
        "Traffic|2012": {
            $sum: "$2012.Traffic"
        },
        "Traffic|2013": {
            $sum: "$2013.Traffic"
        },
        "Traffic|2014": {
            $sum: "$2014.Traffic"
        },
        "Traffic|2015": {
            $sum: "$2015.Traffic"
        },
        "Traffic|2016": {
            $sum: "$2016.Traffic"
        },
        "Traffic|2017": {
            $sum: "$2017.Traffic"
        },
        "Traffic|2018": {
            $sum: "$2018.Traffic"
        },
        "Traffic|2019": {
            $sum: "$2019.Traffic"
        },
        "Traffic|2020": {
            $sum: "$2020.Traffic"
        },
        "Traffic|2021": {
            $sum: "$2021.Traffic"
        },
        "Traffic|2022": {
            $sum: "$2022.Traffic"
        },
        "Traffic|2023": {
            $sum: "$2023.Traffic"
        },
        "Traffic|2024": {
            $sum: "$2024.Traffic"
        },
        "Traffic|2025": {
            $sum: "$2025.Traffic"
        },
        "Traffic|2026": {
            $sum: "$2026.Traffic"
        },
        "Traffic|2027": {
            $sum: "$2027.Traffic"
        },
        "Traffic|2028": {
            $sum: "$2028.Traffic"
        },
        "Traffic|2029": {
            $sum: "$2029.Traffic"
        },
        "Traffic|2030": {
            $sum: "$2030.Traffic"
        },
        "Traffic|2031": {
            $sum: "$2031.Traffic"
        },
        "Traffic|2032": {
            $sum: "$2032.Traffic"
        },
        "Traffic|2033": {
            $sum: "$2033.Traffic"
        },
        "Traffic|2034": {
            $sum: "$2034.Traffic"
        },
        "Traffic|2035": {
            $sum: "$2035.Traffic"
        },
        "Traffic|2036": {
            $sum: "$2036.Traffic"
        },
        "Traffic|2037": {
            $sum: "$2037.Traffic"
        },
        "Traffic|2038": {
            $sum: "$2038.Traffic"
        },
        "Traffic|2039": {
            $sum: "$2039.Traffic"
        },
        "Traffic|2040": {
            $sum: "$2040.Traffic"
        },
        "Traffic|2041": {
            $sum: "$2041.Traffic"
        },
        "Traffic|2042": {
            $sum: "$2042.Traffic"
        },
        "Traffic|2043": {
            $sum: "$2043.Traffic"
        },
        "Traffic|2044": {
            $sum: "$2044.Traffic"
        },
        "Traffic|2045": {
            $sum: "$2045.Traffic"
        },
        "Traffic|2046": {
            $sum: "$2046.Traffic"
        },
        "Traffic|2047": {
            $sum: "$2047.Traffic"
        },
        "Traffic|2048": {
            $sum: "$2048.Traffic"
        },
        "Traffic|2049": {
            $sum: "$2049.Traffic"
        },
        "Traffic|2050": {
            $sum: "$2050.Traffic"
        },
        "Traffic|2051": {
            $sum: "$2051.Traffic"
        },
        "Traffic|2052": {
            $sum: "$2052.Traffic"
        },
        "Traffic|2053": {
            $sum: "$2053.Traffic"
        },
        "Traffic|2054": {
            $sum: "$2054.Traffic"
        },
        "Traffic|2055": {
            $sum: "$2055.Traffic"
        },
        "Traffic|2056": {
            $sum: "$2056.Traffic"
        },
        "Traffic|2057": {
            $sum: "$2057.Traffic"
        },
        "Traffic|2058": {
            $sum: "$2058.Traffic"
        },
        "Traffic|2059": {
            $sum: "$2059.Traffic"
        },
        "Traffic|2100": {
            $sum: "$2100.Traffic"
        },
        "Traffic|2101": {
            $sum: "$2101.Traffic"
        },
        "Traffic|2102": {
            $sum: "$2102.Traffic"
        },
        "Traffic|2103": {
            $sum: "$2103.Traffic"
        },
        "Traffic|2104": {
            $sum: "$2104.Traffic"
        },
        "Traffic|2105": {
            $sum: "$2105.Traffic"
        },
        "Traffic|2106": {
            $sum: "$2106.Traffic"
        },
        "Traffic|2107": {
            $sum: "$2107.Traffic"
        },
        "Traffic|2108": {
            $sum: "$2108.Traffic"
        },
        "Traffic|2109": {
            $sum: "$2109.Traffic"
        },
        "Traffic|2110": {
            $sum: "$2110.Traffic"
        },
        "Traffic|2111": {
            $sum: "$2111.Traffic"
        },
        "Traffic|2112": {
            $sum: "$2112.Traffic"
        },
        "Traffic|2113": {
            $sum: "$2113.Traffic"
        },
        "Traffic|2114": {
            $sum: "$2114.Traffic"
        },
        "Traffic|2115": {
            $sum: "$2115.Traffic"
        },
        "Traffic|2116": {
            $sum: "$2116.Traffic"
        },
        "Traffic|2117": {
            $sum: "$2117.Traffic"
        },
        "Traffic|2118": {
            $sum: "$2118.Traffic"
        },
        "Traffic|2119": {
            $sum: "$2119.Traffic"
        },
        "Traffic|2120": {
            $sum: "$2120.Traffic"
        },
        "Traffic|2121": {
            $sum: "$2121.Traffic"
        },
        "Traffic|2122": {
            $sum: "$2122.Traffic"
        },
        "Traffic|2123": {
            $sum: "$2123.Traffic"
        },
        "Traffic|2124": {
            $sum: "$2124.Traffic"
        },
        "Traffic|2125": {
            $sum: "$2125.Traffic"
        },
        "Traffic|2126": {
            $sum: "$2126.Traffic"
        },
        "Traffic|2127": {
            $sum: "$2127.Traffic"
        },
        "Traffic|2128": {
            $sum: "$2128.Traffic"
        },
        "Traffic|2129": {
            $sum: "$2129.Traffic"
        },
        "Traffic|2130": {
            $sum: "$2130.Traffic"
        },
        "Traffic|2131": {
            $sum: "$2131.Traffic"
        },
        "Traffic|2132": {
            $sum: "$2132.Traffic"
        },
        "Traffic|2133": {
            $sum: "$2133.Traffic"
        },
        "Traffic|2134": {
            $sum: "$2134.Traffic"
        },
        "Traffic|2135": {
            $sum: "$2135.Traffic"
        },
        "Traffic|2136": {
            $sum: "$2136.Traffic"
        },
        "Traffic|2137": {
            $sum: "$2137.Traffic"
        },
        "Traffic|2138": {
            $sum: "$2138.Traffic"
        },
        "Traffic|2139": {
            $sum: "$2139.Traffic"
        },
        "Traffic|2140": {
            $sum: "$2140.Traffic"
        },
        "Traffic|2141": {
            $sum: "$2141.Traffic"
        },
        "Traffic|2142": {
            $sum: "$2142.Traffic"
        },
        "Traffic|2143": {
            $sum: "$2143.Traffic"
        },
        "Traffic|2144": {
            $sum: "$2144.Traffic"
        },
        "Traffic|2145": {
            $sum: "$2145.Traffic"
        },
        "Traffic|2146": {
            $sum: "$2146.Traffic"
        },
        "Traffic|2147": {
            $sum: "$2147.Traffic"
        },
        "Traffic|2148": {
            $sum: "$2148.Traffic"
        },
        "Traffic|2149": {
            $sum: "$2149.Traffic"
        },
        "Traffic|2150": {
            $sum: "$2150.Traffic"
        },
        "Traffic|2151": {
            $sum: "$2151.Traffic"
        },
        "Traffic|2152": {
            $sum: "$2152.Traffic"
        },
        "Traffic|2153": {
            $sum: "$2153.Traffic"
        },
        "Traffic|2154": {
            $sum: "$2154.Traffic"
        },
        "Traffic|2155": {
            $sum: "$2155.Traffic"
        },
        "Traffic|2156": {
            $sum: "$2156.Traffic"
        },
        "Traffic|2157": {
            $sum: "$2157.Traffic"
        },
        "Traffic|2158": {
            $sum: "$2158.Traffic"
        },
        "Traffic|2159": {
            $sum: "$2159.Traffic"
        },
        "Traffic|2200": {
            $sum: "$2200.Traffic"
        },
        "Traffic|2201": {
            $sum: "$2201.Traffic"
        },
        "Traffic|2202": {
            $sum: "$2202.Traffic"
        },
        "Traffic|2203": {
            $sum: "$2203.Traffic"
        },
        "Traffic|2204": {
            $sum: "$2204.Traffic"
        },
        "Traffic|2205": {
            $sum: "$2205.Traffic"
        },
        "Traffic|2206": {
            $sum: "$2206.Traffic"
        },
        "Traffic|2207": {
            $sum: "$2207.Traffic"
        },
        "Traffic|2208": {
            $sum: "$2208.Traffic"
        },
        "Traffic|2209": {
            $sum: "$2209.Traffic"
        },
        "Traffic|2210": {
            $sum: "$2210.Traffic"
        },
        "Traffic|2211": {
            $sum: "$2211.Traffic"
        },
        "Traffic|2212": {
            $sum: "$2212.Traffic"
        },
        "Traffic|2213": {
            $sum: "$2213.Traffic"
        },
        "Traffic|2214": {
            $sum: "$2214.Traffic"
        },
        "Traffic|2215": {
            $sum: "$2215.Traffic"
        },
        "Traffic|2216": {
            $sum: "$2216.Traffic"
        },
        "Traffic|2217": {
            $sum: "$2217.Traffic"
        },
        "Traffic|2218": {
            $sum: "$2218.Traffic"
        },
        "Traffic|2219": {
            $sum: "$2219.Traffic"
        },
        "Traffic|2220": {
            $sum: "$2220.Traffic"
        },
        "Traffic|2221": {
            $sum: "$2221.Traffic"
        },
        "Traffic|2222": {
            $sum: "$2222.Traffic"
        },
        "Traffic|2223": {
            $sum: "$2223.Traffic"
        },
        "Traffic|2224": {
            $sum: "$2224.Traffic"
        },
        "Traffic|2225": {
            $sum: "$2225.Traffic"
        },
        "Traffic|2226": {
            $sum: "$2226.Traffic"
        },
        "Traffic|2227": {
            $sum: "$2227.Traffic"
        },
        "Traffic|2228": {
            $sum: "$2228.Traffic"
        },
        "Traffic|2229": {
            $sum: "$2229.Traffic"
        },
        "Traffic|2230": {
            $sum: "$2230.Traffic"
        },
        "Traffic|2231": {
            $sum: "$2231.Traffic"
        },
        "Traffic|2232": {
            $sum: "$2232.Traffic"
        },
        "Traffic|2233": {
            $sum: "$2233.Traffic"
        },
        "Traffic|2234": {
            $sum: "$2234.Traffic"
        },
        "Traffic|2235": {
            $sum: "$2235.Traffic"
        },
        "Traffic|2236": {
            $sum: "$2236.Traffic"
        },
        "Traffic|2237": {
            $sum: "$2237.Traffic"
        },
        "Traffic|2238": {
            $sum: "$2238.Traffic"
        },
        "Traffic|2239": {
            $sum: "$2239.Traffic"
        },
        "Traffic|2240": {
            $sum: "$2240.Traffic"
        },
        "Traffic|2241": {
            $sum: "$2241.Traffic"
        },
        "Traffic|2242": {
            $sum: "$2242.Traffic"
        },
        "Traffic|2243": {
            $sum: "$2243.Traffic"
        },
        "Traffic|2244": {
            $sum: "$2244.Traffic"
        },
        "Traffic|2245": {
            $sum: "$2245.Traffic"
        },
        "Traffic|2246": {
            $sum: "$2246.Traffic"
        },
        "Traffic|2247": {
            $sum: "$2247.Traffic"
        },
        "Traffic|2248": {
            $sum: "$2248.Traffic"
        },
        "Traffic|2249": {
            $sum: "$2249.Traffic"
        },
        "Traffic|2250": {
            $sum: "$2250.Traffic"
        },
        "Traffic|2251": {
            $sum: "$2251.Traffic"
        },
        "Traffic|2252": {
            $sum: "$2252.Traffic"
        },
        "Traffic|2253": {
            $sum: "$2253.Traffic"
        },
        "Traffic|2254": {
            $sum: "$2254.Traffic"
        },
        "Traffic|2255": {
            $sum: "$2255.Traffic"
        },
        "Traffic|2256": {
            $sum: "$2256.Traffic"
        },
        "Traffic|2257": {
            $sum: "$2257.Traffic"
        },
        "Traffic|2258": {
            $sum: "$2258.Traffic"
        },
        "Traffic|2259": {
            $sum: "$2259.Traffic"
        },
        "Traffic|2300": {
            $sum: "$2300.Traffic"
        },
        "Traffic|2301": {
            $sum: "$2301.Traffic"
        },
        "Traffic|2302": {
            $sum: "$2302.Traffic"
        },
        "Traffic|2303": {
            $sum: "$2303.Traffic"
        },
        "Traffic|2304": {
            $sum: "$2304.Traffic"
        },
        "Traffic|2305": {
            $sum: "$2305.Traffic"
        },
        "Traffic|2306": {
            $sum: "$2306.Traffic"
        },
        "Traffic|2307": {
            $sum: "$2307.Traffic"
        },
        "Traffic|2308": {
            $sum: "$2308.Traffic"
        },
        "Traffic|2309": {
            $sum: "$2309.Traffic"
        },
        "Traffic|2310": {
            $sum: "$2310.Traffic"
        },
        "Traffic|2311": {
            $sum: "$2311.Traffic"
        },
        "Traffic|2312": {
            $sum: "$2312.Traffic"
        },
        "Traffic|2313": {
            $sum: "$2313.Traffic"
        },
        "Traffic|2314": {
            $sum: "$2314.Traffic"
        },
        "Traffic|2315": {
            $sum: "$2315.Traffic"
        },
        "Traffic|2316": {
            $sum: "$2316.Traffic"
        },
        "Traffic|2317": {
            $sum: "$2317.Traffic"
        },
        "Traffic|2318": {
            $sum: "$2318.Traffic"
        },
        "Traffic|2319": {
            $sum: "$2319.Traffic"
        },
        "Traffic|2320": {
            $sum: "$2320.Traffic"
        },
        "Traffic|2321": {
            $sum: "$2321.Traffic"
        },
        "Traffic|2322": {
            $sum: "$2322.Traffic"
        },
        "Traffic|2323": {
            $sum: "$2323.Traffic"
        },
        "Traffic|2324": {
            $sum: "$2324.Traffic"
        },
        "Traffic|2325": {
            $sum: "$2325.Traffic"
        },
        "Traffic|2326": {
            $sum: "$2326.Traffic"
        },
        "Traffic|2327": {
            $sum: "$2327.Traffic"
        },
        "Traffic|2328": {
            $sum: "$2328.Traffic"
        },
        "Traffic|2329": {
            $sum: "$2329.Traffic"
        },
        "Traffic|2330": {
            $sum: "$2330.Traffic"
        },
        "Traffic|2331": {
            $sum: "$2331.Traffic"
        },
        "Traffic|2332": {
            $sum: "$2332.Traffic"
        },
        "Traffic|2333": {
            $sum: "$2333.Traffic"
        },
        "Traffic|2334": {
            $sum: "$2334.Traffic"
        },
        "Traffic|2335": {
            $sum: "$2335.Traffic"
        },
        "Traffic|2336": {
            $sum: "$2336.Traffic"
        },
        "Traffic|2337": {
            $sum: "$2337.Traffic"
        },
        "Traffic|2338": {
            $sum: "$2338.Traffic"
        },
        "Traffic|2339": {
            $sum: "$2339.Traffic"
        },
        "Traffic|2340": {
            $sum: "$2340.Traffic"
        },
        "Traffic|2341": {
            $sum: "$2341.Traffic"
        },
        "Traffic|2342": {
            $sum: "$2342.Traffic"
        },
        "Traffic|2343": {
            $sum: "$2343.Traffic"
        },
        "Traffic|2344": {
            $sum: "$2344.Traffic"
        },
        "Traffic|2345": {
            $sum: "$2345.Traffic"
        },
        "Traffic|2346": {
            $sum: "$2346.Traffic"
        },
        "Traffic|2347": {
            $sum: "$2347.Traffic"
        },
        "Traffic|2348": {
            $sum: "$2348.Traffic"
        },
        "Traffic|2349": {
            $sum: "$2349.Traffic"
        },
        "Traffic|2350": {
            $sum: "$2350.Traffic"
        },
        "Traffic|2351": {
            $sum: "$2351.Traffic"
        },
        "Traffic|2352": {
            $sum: "$2352.Traffic"
        },
        "Traffic|2353": {
            $sum: "$2353.Traffic"
        },
        "Traffic|2354": {
            $sum: "$2354.Traffic"
        },
        "Traffic|2355": {
            $sum: "$2355.Traffic"
        },
        "Traffic|2356": {
            $sum: "$2356.Traffic"
        },
        "Traffic|2357": {
            $sum: "$2357.Traffic"
        },
        "Traffic|2358": {
            $sum: "$2358.Traffic"
        },
        "Traffic|2359": {
            $sum: "$2359.Traffic"
        },
        "HttpsTraffic|0000": {
            $sum: "$0000.HttpsTraffic"
        },
        "HttpsTraffic|0001": {
            $sum: "$0001.HttpsTraffic"
        },
        "HttpsTraffic|0002": {
            $sum: "$0002.HttpsTraffic"
        },
        "HttpsTraffic|0003": {
            $sum: "$0003.HttpsTraffic"
        },
        "HttpsTraffic|0004": {
            $sum: "$0004.HttpsTraffic"
        },
        "HttpsTraffic|0005": {
            $sum: "$0005.HttpsTraffic"
        },
        "HttpsTraffic|0006": {
            $sum: "$0006.HttpsTraffic"
        },
        "HttpsTraffic|0007": {
            $sum: "$0007.HttpsTraffic"
        },
        "HttpsTraffic|0008": {
            $sum: "$0008.HttpsTraffic"
        },
        "HttpsTraffic|0009": {
            $sum: "$0009.HttpsTraffic"
        },
        "HttpsTraffic|0010": {
            $sum: "$0010.HttpsTraffic"
        },
        "HttpsTraffic|0011": {
            $sum: "$0011.HttpsTraffic"
        },
        "HttpsTraffic|0012": {
            $sum: "$0012.HttpsTraffic"
        },
        "HttpsTraffic|0013": {
            $sum: "$0013.HttpsTraffic"
        },
        "HttpsTraffic|0014": {
            $sum: "$0014.HttpsTraffic"
        },
        "HttpsTraffic|0015": {
            $sum: "$0015.HttpsTraffic"
        },
        "HttpsTraffic|0016": {
            $sum: "$0016.HttpsTraffic"
        },
        "HttpsTraffic|0017": {
            $sum: "$0017.HttpsTraffic"
        },
        "HttpsTraffic|0018": {
            $sum: "$0018.HttpsTraffic"
        },
        "HttpsTraffic|0019": {
            $sum: "$0019.HttpsTraffic"
        },
        "HttpsTraffic|0020": {
            $sum: "$0020.HttpsTraffic"
        },
        "HttpsTraffic|0021": {
            $sum: "$0021.HttpsTraffic"
        },
        "HttpsTraffic|0022": {
            $sum: "$0022.HttpsTraffic"
        },
        "HttpsTraffic|0023": {
            $sum: "$0023.HttpsTraffic"
        },
        "HttpsTraffic|0024": {
            $sum: "$0024.HttpsTraffic"
        },
        "HttpsTraffic|0025": {
            $sum: "$0025.HttpsTraffic"
        },
        "HttpsTraffic|0026": {
            $sum: "$0026.HttpsTraffic"
        },
        "HttpsTraffic|0027": {
            $sum: "$0027.HttpsTraffic"
        },
        "HttpsTraffic|0028": {
            $sum: "$0028.HttpsTraffic"
        },
        "HttpsTraffic|0029": {
            $sum: "$0029.HttpsTraffic"
        },
        "HttpsTraffic|0030": {
            $sum: "$0030.HttpsTraffic"
        },
        "HttpsTraffic|0031": {
            $sum: "$0031.HttpsTraffic"
        },
        "HttpsTraffic|0032": {
            $sum: "$0032.HttpsTraffic"
        },
        "HttpsTraffic|0033": {
            $sum: "$0033.HttpsTraffic"
        },
        "HttpsTraffic|0034": {
            $sum: "$0034.HttpsTraffic"
        },
        "HttpsTraffic|0035": {
            $sum: "$0035.HttpsTraffic"
        },
        "HttpsTraffic|0036": {
            $sum: "$0036.HttpsTraffic"
        },
        "HttpsTraffic|0037": {
            $sum: "$0037.HttpsTraffic"
        },
        "HttpsTraffic|0038": {
            $sum: "$0038.HttpsTraffic"
        },
        "HttpsTraffic|0039": {
            $sum: "$0039.HttpsTraffic"
        },
        "HttpsTraffic|0040": {
            $sum: "$0040.HttpsTraffic"
        },
        "HttpsTraffic|0041": {
            $sum: "$0041.HttpsTraffic"
        },
        "HttpsTraffic|0042": {
            $sum: "$0042.HttpsTraffic"
        },
        "HttpsTraffic|0043": {
            $sum: "$0043.HttpsTraffic"
        },
        "HttpsTraffic|0044": {
            $sum: "$0044.HttpsTraffic"
        },
        "HttpsTraffic|0045": {
            $sum: "$0045.HttpsTraffic"
        },
        "HttpsTraffic|0046": {
            $sum: "$0046.HttpsTraffic"
        },
        "HttpsTraffic|0047": {
            $sum: "$0047.HttpsTraffic"
        },
        "HttpsTraffic|0048": {
            $sum: "$0048.HttpsTraffic"
        },
        "HttpsTraffic|0049": {
            $sum: "$0049.HttpsTraffic"
        },
        "HttpsTraffic|0050": {
            $sum: "$0050.HttpsTraffic"
        },
        "HttpsTraffic|0051": {
            $sum: "$0051.HttpsTraffic"
        },
        "HttpsTraffic|0052": {
            $sum: "$0052.HttpsTraffic"
        },
        "HttpsTraffic|0053": {
            $sum: "$0053.HttpsTraffic"
        },
        "HttpsTraffic|0054": {
            $sum: "$0054.HttpsTraffic"
        },
        "HttpsTraffic|0055": {
            $sum: "$0055.HttpsTraffic"
        },
        "HttpsTraffic|0056": {
            $sum: "$0056.HttpsTraffic"
        },
        "HttpsTraffic|0057": {
            $sum: "$0057.HttpsTraffic"
        },
        "HttpsTraffic|0058": {
            $sum: "$0058.HttpsTraffic"
        },
        "HttpsTraffic|0059": {
            $sum: "$0059.HttpsTraffic"
        },
        "HttpsTraffic|0100": {
            $sum: "$0100.HttpsTraffic"
        },
        "HttpsTraffic|0101": {
            $sum: "$0101.HttpsTraffic"
        },
        "HttpsTraffic|0102": {
            $sum: "$0102.HttpsTraffic"
        },
        "HttpsTraffic|0103": {
            $sum: "$0103.HttpsTraffic"
        },
        "HttpsTraffic|0104": {
            $sum: "$0104.HttpsTraffic"
        },
        "HttpsTraffic|0105": {
            $sum: "$0105.HttpsTraffic"
        },
        "HttpsTraffic|0106": {
            $sum: "$0106.HttpsTraffic"
        },
        "HttpsTraffic|0107": {
            $sum: "$0107.HttpsTraffic"
        },
        "HttpsTraffic|0108": {
            $sum: "$0108.HttpsTraffic"
        },
        "HttpsTraffic|0109": {
            $sum: "$0109.HttpsTraffic"
        },
        "HttpsTraffic|0110": {
            $sum: "$0110.HttpsTraffic"
        },
        "HttpsTraffic|0111": {
            $sum: "$0111.HttpsTraffic"
        },
        "HttpsTraffic|0112": {
            $sum: "$0112.HttpsTraffic"
        },
        "HttpsTraffic|0113": {
            $sum: "$0113.HttpsTraffic"
        },
        "HttpsTraffic|0114": {
            $sum: "$0114.HttpsTraffic"
        },
        "HttpsTraffic|0115": {
            $sum: "$0115.HttpsTraffic"
        },
        "HttpsTraffic|0116": {
            $sum: "$0116.HttpsTraffic"
        },
        "HttpsTraffic|0117": {
            $sum: "$0117.HttpsTraffic"
        },
        "HttpsTraffic|0118": {
            $sum: "$0118.HttpsTraffic"
        },
        "HttpsTraffic|0119": {
            $sum: "$0119.HttpsTraffic"
        },
        "HttpsTraffic|0120": {
            $sum: "$0120.HttpsTraffic"
        },
        "HttpsTraffic|0121": {
            $sum: "$0121.HttpsTraffic"
        },
        "HttpsTraffic|0122": {
            $sum: "$0122.HttpsTraffic"
        },
        "HttpsTraffic|0123": {
            $sum: "$0123.HttpsTraffic"
        },
        "HttpsTraffic|0124": {
            $sum: "$0124.HttpsTraffic"
        },
        "HttpsTraffic|0125": {
            $sum: "$0125.HttpsTraffic"
        },
        "HttpsTraffic|0126": {
            $sum: "$0126.HttpsTraffic"
        },
        "HttpsTraffic|0127": {
            $sum: "$0127.HttpsTraffic"
        },
        "HttpsTraffic|0128": {
            $sum: "$0128.HttpsTraffic"
        },
        "HttpsTraffic|0129": {
            $sum: "$0129.HttpsTraffic"
        },
        "HttpsTraffic|0130": {
            $sum: "$0130.HttpsTraffic"
        },
        "HttpsTraffic|0131": {
            $sum: "$0131.HttpsTraffic"
        },
        "HttpsTraffic|0132": {
            $sum: "$0132.HttpsTraffic"
        },
        "HttpsTraffic|0133": {
            $sum: "$0133.HttpsTraffic"
        },
        "HttpsTraffic|0134": {
            $sum: "$0134.HttpsTraffic"
        },
        "HttpsTraffic|0135": {
            $sum: "$0135.HttpsTraffic"
        },
        "HttpsTraffic|0136": {
            $sum: "$0136.HttpsTraffic"
        },
        "HttpsTraffic|0137": {
            $sum: "$0137.HttpsTraffic"
        },
        "HttpsTraffic|0138": {
            $sum: "$0138.HttpsTraffic"
        },
        "HttpsTraffic|0139": {
            $sum: "$0139.HttpsTraffic"
        },
        "HttpsTraffic|0140": {
            $sum: "$0140.HttpsTraffic"
        },
        "HttpsTraffic|0141": {
            $sum: "$0141.HttpsTraffic"
        },
        "HttpsTraffic|0142": {
            $sum: "$0142.HttpsTraffic"
        },
        "HttpsTraffic|0143": {
            $sum: "$0143.HttpsTraffic"
        },
        "HttpsTraffic|0144": {
            $sum: "$0144.HttpsTraffic"
        },
        "HttpsTraffic|0145": {
            $sum: "$0145.HttpsTraffic"
        },
        "HttpsTraffic|0146": {
            $sum: "$0146.HttpsTraffic"
        },
        "HttpsTraffic|0147": {
            $sum: "$0147.HttpsTraffic"
        },
        "HttpsTraffic|0148": {
            $sum: "$0148.HttpsTraffic"
        },
        "HttpsTraffic|0149": {
            $sum: "$0149.HttpsTraffic"
        },
        "HttpsTraffic|0150": {
            $sum: "$0150.HttpsTraffic"
        },
        "HttpsTraffic|0151": {
            $sum: "$0151.HttpsTraffic"
        },
        "HttpsTraffic|0152": {
            $sum: "$0152.HttpsTraffic"
        },
        "HttpsTraffic|0153": {
            $sum: "$0153.HttpsTraffic"
        },
        "HttpsTraffic|0154": {
            $sum: "$0154.HttpsTraffic"
        },
        "HttpsTraffic|0155": {
            $sum: "$0155.HttpsTraffic"
        },
        "HttpsTraffic|0156": {
            $sum: "$0156.HttpsTraffic"
        },
        "HttpsTraffic|0157": {
            $sum: "$0157.HttpsTraffic"
        },
        "HttpsTraffic|0158": {
            $sum: "$0158.HttpsTraffic"
        },
        "HttpsTraffic|0159": {
            $sum: "$0159.HttpsTraffic"
        },
        "HttpsTraffic|0200": {
            $sum: "$0200.HttpsTraffic"
        },
        "HttpsTraffic|0201": {
            $sum: "$0201.HttpsTraffic"
        },
        "HttpsTraffic|0202": {
            $sum: "$0202.HttpsTraffic"
        },
        "HttpsTraffic|0203": {
            $sum: "$0203.HttpsTraffic"
        },
        "HttpsTraffic|0204": {
            $sum: "$0204.HttpsTraffic"
        },
        "HttpsTraffic|0205": {
            $sum: "$0205.HttpsTraffic"
        },
        "HttpsTraffic|0206": {
            $sum: "$0206.HttpsTraffic"
        },
        "HttpsTraffic|0207": {
            $sum: "$0207.HttpsTraffic"
        },
        "HttpsTraffic|0208": {
            $sum: "$0208.HttpsTraffic"
        },
        "HttpsTraffic|0209": {
            $sum: "$0209.HttpsTraffic"
        },
        "HttpsTraffic|0210": {
            $sum: "$0210.HttpsTraffic"
        },
        "HttpsTraffic|0211": {
            $sum: "$0211.HttpsTraffic"
        },
        "HttpsTraffic|0212": {
            $sum: "$0212.HttpsTraffic"
        },
        "HttpsTraffic|0213": {
            $sum: "$0213.HttpsTraffic"
        },
        "HttpsTraffic|0214": {
            $sum: "$0214.HttpsTraffic"
        },
        "HttpsTraffic|0215": {
            $sum: "$0215.HttpsTraffic"
        },
        "HttpsTraffic|0216": {
            $sum: "$0216.HttpsTraffic"
        },
        "HttpsTraffic|0217": {
            $sum: "$0217.HttpsTraffic"
        },
        "HttpsTraffic|0218": {
            $sum: "$0218.HttpsTraffic"
        },
        "HttpsTraffic|0219": {
            $sum: "$0219.HttpsTraffic"
        },
        "HttpsTraffic|0220": {
            $sum: "$0220.HttpsTraffic"
        },
        "HttpsTraffic|0221": {
            $sum: "$0221.HttpsTraffic"
        },
        "HttpsTraffic|0222": {
            $sum: "$0222.HttpsTraffic"
        },
        "HttpsTraffic|0223": {
            $sum: "$0223.HttpsTraffic"
        },
        "HttpsTraffic|0224": {
            $sum: "$0224.HttpsTraffic"
        },
        "HttpsTraffic|0225": {
            $sum: "$0225.HttpsTraffic"
        },
        "HttpsTraffic|0226": {
            $sum: "$0226.HttpsTraffic"
        },
        "HttpsTraffic|0227": {
            $sum: "$0227.HttpsTraffic"
        },
        "HttpsTraffic|0228": {
            $sum: "$0228.HttpsTraffic"
        },
        "HttpsTraffic|0229": {
            $sum: "$0229.HttpsTraffic"
        },
        "HttpsTraffic|0230": {
            $sum: "$0230.HttpsTraffic"
        },
        "HttpsTraffic|0231": {
            $sum: "$0231.HttpsTraffic"
        },
        "HttpsTraffic|0232": {
            $sum: "$0232.HttpsTraffic"
        },
        "HttpsTraffic|0233": {
            $sum: "$0233.HttpsTraffic"
        },
        "HttpsTraffic|0234": {
            $sum: "$0234.HttpsTraffic"
        },
        "HttpsTraffic|0235": {
            $sum: "$0235.HttpsTraffic"
        },
        "HttpsTraffic|0236": {
            $sum: "$0236.HttpsTraffic"
        },
        "HttpsTraffic|0237": {
            $sum: "$0237.HttpsTraffic"
        },
        "HttpsTraffic|0238": {
            $sum: "$0238.HttpsTraffic"
        },
        "HttpsTraffic|0239": {
            $sum: "$0239.HttpsTraffic"
        },
        "HttpsTraffic|0240": {
            $sum: "$0240.HttpsTraffic"
        },
        "HttpsTraffic|0241": {
            $sum: "$0241.HttpsTraffic"
        },
        "HttpsTraffic|0242": {
            $sum: "$0242.HttpsTraffic"
        },
        "HttpsTraffic|0243": {
            $sum: "$0243.HttpsTraffic"
        },
        "HttpsTraffic|0244": {
            $sum: "$0244.HttpsTraffic"
        },
        "HttpsTraffic|0245": {
            $sum: "$0245.HttpsTraffic"
        },
        "HttpsTraffic|0246": {
            $sum: "$0246.HttpsTraffic"
        },
        "HttpsTraffic|0247": {
            $sum: "$0247.HttpsTraffic"
        },
        "HttpsTraffic|0248": {
            $sum: "$0248.HttpsTraffic"
        },
        "HttpsTraffic|0249": {
            $sum: "$0249.HttpsTraffic"
        },
        "HttpsTraffic|0250": {
            $sum: "$0250.HttpsTraffic"
        },
        "HttpsTraffic|0251": {
            $sum: "$0251.HttpsTraffic"
        },
        "HttpsTraffic|0252": {
            $sum: "$0252.HttpsTraffic"
        },
        "HttpsTraffic|0253": {
            $sum: "$0253.HttpsTraffic"
        },
        "HttpsTraffic|0254": {
            $sum: "$0254.HttpsTraffic"
        },
        "HttpsTraffic|0255": {
            $sum: "$0255.HttpsTraffic"
        },
        "HttpsTraffic|0256": {
            $sum: "$0256.HttpsTraffic"
        },
        "HttpsTraffic|0257": {
            $sum: "$0257.HttpsTraffic"
        },
        "HttpsTraffic|0258": {
            $sum: "$0258.HttpsTraffic"
        },
        "HttpsTraffic|0259": {
            $sum: "$0259.HttpsTraffic"
        },
        "HttpsTraffic|0300": {
            $sum: "$0300.HttpsTraffic"
        },
        "HttpsTraffic|0301": {
            $sum: "$0301.HttpsTraffic"
        },
        "HttpsTraffic|0302": {
            $sum: "$0302.HttpsTraffic"
        },
        "HttpsTraffic|0303": {
            $sum: "$0303.HttpsTraffic"
        },
        "HttpsTraffic|0304": {
            $sum: "$0304.HttpsTraffic"
        },
        "HttpsTraffic|0305": {
            $sum: "$0305.HttpsTraffic"
        },
        "HttpsTraffic|0306": {
            $sum: "$0306.HttpsTraffic"
        },
        "HttpsTraffic|0307": {
            $sum: "$0307.HttpsTraffic"
        },
        "HttpsTraffic|0308": {
            $sum: "$0308.HttpsTraffic"
        },
        "HttpsTraffic|0309": {
            $sum: "$0309.HttpsTraffic"
        },
        "HttpsTraffic|0310": {
            $sum: "$0310.HttpsTraffic"
        },
        "HttpsTraffic|0311": {
            $sum: "$0311.HttpsTraffic"
        },
        "HttpsTraffic|0312": {
            $sum: "$0312.HttpsTraffic"
        },
        "HttpsTraffic|0313": {
            $sum: "$0313.HttpsTraffic"
        },
        "HttpsTraffic|0314": {
            $sum: "$0314.HttpsTraffic"
        },
        "HttpsTraffic|0315": {
            $sum: "$0315.HttpsTraffic"
        },
        "HttpsTraffic|0316": {
            $sum: "$0316.HttpsTraffic"
        },
        "HttpsTraffic|0317": {
            $sum: "$0317.HttpsTraffic"
        },
        "HttpsTraffic|0318": {
            $sum: "$0318.HttpsTraffic"
        },
        "HttpsTraffic|0319": {
            $sum: "$0319.HttpsTraffic"
        },
        "HttpsTraffic|0320": {
            $sum: "$0320.HttpsTraffic"
        },
        "HttpsTraffic|0321": {
            $sum: "$0321.HttpsTraffic"
        },
        "HttpsTraffic|0322": {
            $sum: "$0322.HttpsTraffic"
        },
        "HttpsTraffic|0323": {
            $sum: "$0323.HttpsTraffic"
        },
        "HttpsTraffic|0324": {
            $sum: "$0324.HttpsTraffic"
        },
        "HttpsTraffic|0325": {
            $sum: "$0325.HttpsTraffic"
        },
        "HttpsTraffic|0326": {
            $sum: "$0326.HttpsTraffic"
        },
        "HttpsTraffic|0327": {
            $sum: "$0327.HttpsTraffic"
        },
        "HttpsTraffic|0328": {
            $sum: "$0328.HttpsTraffic"
        },
        "HttpsTraffic|0329": {
            $sum: "$0329.HttpsTraffic"
        },
        "HttpsTraffic|0330": {
            $sum: "$0330.HttpsTraffic"
        },
        "HttpsTraffic|0331": {
            $sum: "$0331.HttpsTraffic"
        },
        "HttpsTraffic|0332": {
            $sum: "$0332.HttpsTraffic"
        },
        "HttpsTraffic|0333": {
            $sum: "$0333.HttpsTraffic"
        },
        "HttpsTraffic|0334": {
            $sum: "$0334.HttpsTraffic"
        },
        "HttpsTraffic|0335": {
            $sum: "$0335.HttpsTraffic"
        },
        "HttpsTraffic|0336": {
            $sum: "$0336.HttpsTraffic"
        },
        "HttpsTraffic|0337": {
            $sum: "$0337.HttpsTraffic"
        },
        "HttpsTraffic|0338": {
            $sum: "$0338.HttpsTraffic"
        },
        "HttpsTraffic|0339": {
            $sum: "$0339.HttpsTraffic"
        },
        "HttpsTraffic|0340": {
            $sum: "$0340.HttpsTraffic"
        },
        "HttpsTraffic|0341": {
            $sum: "$0341.HttpsTraffic"
        },
        "HttpsTraffic|0342": {
            $sum: "$0342.HttpsTraffic"
        },
        "HttpsTraffic|0343": {
            $sum: "$0343.HttpsTraffic"
        },
        "HttpsTraffic|0344": {
            $sum: "$0344.HttpsTraffic"
        },
        "HttpsTraffic|0345": {
            $sum: "$0345.HttpsTraffic"
        },
        "HttpsTraffic|0346": {
            $sum: "$0346.HttpsTraffic"
        },
        "HttpsTraffic|0347": {
            $sum: "$0347.HttpsTraffic"
        },
        "HttpsTraffic|0348": {
            $sum: "$0348.HttpsTraffic"
        },
        "HttpsTraffic|0349": {
            $sum: "$0349.HttpsTraffic"
        },
        "HttpsTraffic|0350": {
            $sum: "$0350.HttpsTraffic"
        },
        "HttpsTraffic|0351": {
            $sum: "$0351.HttpsTraffic"
        },
        "HttpsTraffic|0352": {
            $sum: "$0352.HttpsTraffic"
        },
        "HttpsTraffic|0353": {
            $sum: "$0353.HttpsTraffic"
        },
        "HttpsTraffic|0354": {
            $sum: "$0354.HttpsTraffic"
        },
        "HttpsTraffic|0355": {
            $sum: "$0355.HttpsTraffic"
        },
        "HttpsTraffic|0356": {
            $sum: "$0356.HttpsTraffic"
        },
        "HttpsTraffic|0357": {
            $sum: "$0357.HttpsTraffic"
        },
        "HttpsTraffic|0358": {
            $sum: "$0358.HttpsTraffic"
        },
        "HttpsTraffic|0359": {
            $sum: "$0359.HttpsTraffic"
        },
        "HttpsTraffic|0400": {
            $sum: "$0400.HttpsTraffic"
        },
        "HttpsTraffic|0401": {
            $sum: "$0401.HttpsTraffic"
        },
        "HttpsTraffic|0402": {
            $sum: "$0402.HttpsTraffic"
        },
        "HttpsTraffic|0403": {
            $sum: "$0403.HttpsTraffic"
        },
        "HttpsTraffic|0404": {
            $sum: "$0404.HttpsTraffic"
        },
        "HttpsTraffic|0405": {
            $sum: "$0405.HttpsTraffic"
        },
        "HttpsTraffic|0406": {
            $sum: "$0406.HttpsTraffic"
        },
        "HttpsTraffic|0407": {
            $sum: "$0407.HttpsTraffic"
        },
        "HttpsTraffic|0408": {
            $sum: "$0408.HttpsTraffic"
        },
        "HttpsTraffic|0409": {
            $sum: "$0409.HttpsTraffic"
        },
        "HttpsTraffic|0410": {
            $sum: "$0410.HttpsTraffic"
        },
        "HttpsTraffic|0411": {
            $sum: "$0411.HttpsTraffic"
        },
        "HttpsTraffic|0412": {
            $sum: "$0412.HttpsTraffic"
        },
        "HttpsTraffic|0413": {
            $sum: "$0413.HttpsTraffic"
        },
        "HttpsTraffic|0414": {
            $sum: "$0414.HttpsTraffic"
        },
        "HttpsTraffic|0415": {
            $sum: "$0415.HttpsTraffic"
        },
        "HttpsTraffic|0416": {
            $sum: "$0416.HttpsTraffic"
        },
        "HttpsTraffic|0417": {
            $sum: "$0417.HttpsTraffic"
        },
        "HttpsTraffic|0418": {
            $sum: "$0418.HttpsTraffic"
        },
        "HttpsTraffic|0419": {
            $sum: "$0419.HttpsTraffic"
        },
        "HttpsTraffic|0420": {
            $sum: "$0420.HttpsTraffic"
        },
        "HttpsTraffic|0421": {
            $sum: "$0421.HttpsTraffic"
        },
        "HttpsTraffic|0422": {
            $sum: "$0422.HttpsTraffic"
        },
        "HttpsTraffic|0423": {
            $sum: "$0423.HttpsTraffic"
        },
        "HttpsTraffic|0424": {
            $sum: "$0424.HttpsTraffic"
        },
        "HttpsTraffic|0425": {
            $sum: "$0425.HttpsTraffic"
        },
        "HttpsTraffic|0426": {
            $sum: "$0426.HttpsTraffic"
        },
        "HttpsTraffic|0427": {
            $sum: "$0427.HttpsTraffic"
        },
        "HttpsTraffic|0428": {
            $sum: "$0428.HttpsTraffic"
        },
        "HttpsTraffic|0429": {
            $sum: "$0429.HttpsTraffic"
        },
        "HttpsTraffic|0430": {
            $sum: "$0430.HttpsTraffic"
        },
        "HttpsTraffic|0431": {
            $sum: "$0431.HttpsTraffic"
        },
        "HttpsTraffic|0432": {
            $sum: "$0432.HttpsTraffic"
        },
        "HttpsTraffic|0433": {
            $sum: "$0433.HttpsTraffic"
        },
        "HttpsTraffic|0434": {
            $sum: "$0434.HttpsTraffic"
        },
        "HttpsTraffic|0435": {
            $sum: "$0435.HttpsTraffic"
        },
        "HttpsTraffic|0436": {
            $sum: "$0436.HttpsTraffic"
        },
        "HttpsTraffic|0437": {
            $sum: "$0437.HttpsTraffic"
        },
        "HttpsTraffic|0438": {
            $sum: "$0438.HttpsTraffic"
        },
        "HttpsTraffic|0439": {
            $sum: "$0439.HttpsTraffic"
        },
        "HttpsTraffic|0440": {
            $sum: "$0440.HttpsTraffic"
        },
        "HttpsTraffic|0441": {
            $sum: "$0441.HttpsTraffic"
        },
        "HttpsTraffic|0442": {
            $sum: "$0442.HttpsTraffic"
        },
        "HttpsTraffic|0443": {
            $sum: "$0443.HttpsTraffic"
        },
        "HttpsTraffic|0444": {
            $sum: "$0444.HttpsTraffic"
        },
        "HttpsTraffic|0445": {
            $sum: "$0445.HttpsTraffic"
        },
        "HttpsTraffic|0446": {
            $sum: "$0446.HttpsTraffic"
        },
        "HttpsTraffic|0447": {
            $sum: "$0447.HttpsTraffic"
        },
        "HttpsTraffic|0448": {
            $sum: "$0448.HttpsTraffic"
        },
        "HttpsTraffic|0449": {
            $sum: "$0449.HttpsTraffic"
        },
        "HttpsTraffic|0450": {
            $sum: "$0450.HttpsTraffic"
        },
        "HttpsTraffic|0451": {
            $sum: "$0451.HttpsTraffic"
        },
        "HttpsTraffic|0452": {
            $sum: "$0452.HttpsTraffic"
        },
        "HttpsTraffic|0453": {
            $sum: "$0453.HttpsTraffic"
        },
        "HttpsTraffic|0454": {
            $sum: "$0454.HttpsTraffic"
        },
        "HttpsTraffic|0455": {
            $sum: "$0455.HttpsTraffic"
        },
        "HttpsTraffic|0456": {
            $sum: "$0456.HttpsTraffic"
        },
        "HttpsTraffic|0457": {
            $sum: "$0457.HttpsTraffic"
        },
        "HttpsTraffic|0458": {
            $sum: "$0458.HttpsTraffic"
        },
        "HttpsTraffic|0459": {
            $sum: "$0459.HttpsTraffic"
        },
        "HttpsTraffic|0500": {
            $sum: "$0500.HttpsTraffic"
        },
        "HttpsTraffic|0501": {
            $sum: "$0501.HttpsTraffic"
        },
        "HttpsTraffic|0502": {
            $sum: "$0502.HttpsTraffic"
        },
        "HttpsTraffic|0503": {
            $sum: "$0503.HttpsTraffic"
        },
        "HttpsTraffic|0504": {
            $sum: "$0504.HttpsTraffic"
        },
        "HttpsTraffic|0505": {
            $sum: "$0505.HttpsTraffic"
        },
        "HttpsTraffic|0506": {
            $sum: "$0506.HttpsTraffic"
        },
        "HttpsTraffic|0507": {
            $sum: "$0507.HttpsTraffic"
        },
        "HttpsTraffic|0508": {
            $sum: "$0508.HttpsTraffic"
        },
        "HttpsTraffic|0509": {
            $sum: "$0509.HttpsTraffic"
        },
        "HttpsTraffic|0510": {
            $sum: "$0510.HttpsTraffic"
        },
        "HttpsTraffic|0511": {
            $sum: "$0511.HttpsTraffic"
        },
        "HttpsTraffic|0512": {
            $sum: "$0512.HttpsTraffic"
        },
        "HttpsTraffic|0513": {
            $sum: "$0513.HttpsTraffic"
        },
        "HttpsTraffic|0514": {
            $sum: "$0514.HttpsTraffic"
        },
        "HttpsTraffic|0515": {
            $sum: "$0515.HttpsTraffic"
        },
        "HttpsTraffic|0516": {
            $sum: "$0516.HttpsTraffic"
        },
        "HttpsTraffic|0517": {
            $sum: "$0517.HttpsTraffic"
        },
        "HttpsTraffic|0518": {
            $sum: "$0518.HttpsTraffic"
        },
        "HttpsTraffic|0519": {
            $sum: "$0519.HttpsTraffic"
        },
        "HttpsTraffic|0520": {
            $sum: "$0520.HttpsTraffic"
        },
        "HttpsTraffic|0521": {
            $sum: "$0521.HttpsTraffic"
        },
        "HttpsTraffic|0522": {
            $sum: "$0522.HttpsTraffic"
        },
        "HttpsTraffic|0523": {
            $sum: "$0523.HttpsTraffic"
        },
        "HttpsTraffic|0524": {
            $sum: "$0524.HttpsTraffic"
        },
        "HttpsTraffic|0525": {
            $sum: "$0525.HttpsTraffic"
        },
        "HttpsTraffic|0526": {
            $sum: "$0526.HttpsTraffic"
        },
        "HttpsTraffic|0527": {
            $sum: "$0527.HttpsTraffic"
        },
        "HttpsTraffic|0528": {
            $sum: "$0528.HttpsTraffic"
        },
        "HttpsTraffic|0529": {
            $sum: "$0529.HttpsTraffic"
        },
        "HttpsTraffic|0530": {
            $sum: "$0530.HttpsTraffic"
        },
        "HttpsTraffic|0531": {
            $sum: "$0531.HttpsTraffic"
        },
        "HttpsTraffic|0532": {
            $sum: "$0532.HttpsTraffic"
        },
        "HttpsTraffic|0533": {
            $sum: "$0533.HttpsTraffic"
        },
        "HttpsTraffic|0534": {
            $sum: "$0534.HttpsTraffic"
        },
        "HttpsTraffic|0535": {
            $sum: "$0535.HttpsTraffic"
        },
        "HttpsTraffic|0536": {
            $sum: "$0536.HttpsTraffic"
        },
        "HttpsTraffic|0537": {
            $sum: "$0537.HttpsTraffic"
        },
        "HttpsTraffic|0538": {
            $sum: "$0538.HttpsTraffic"
        },
        "HttpsTraffic|0539": {
            $sum: "$0539.HttpsTraffic"
        },
        "HttpsTraffic|0540": {
            $sum: "$0540.HttpsTraffic"
        },
        "HttpsTraffic|0541": {
            $sum: "$0541.HttpsTraffic"
        },
        "HttpsTraffic|0542": {
            $sum: "$0542.HttpsTraffic"
        },
        "HttpsTraffic|0543": {
            $sum: "$0543.HttpsTraffic"
        },
        "HttpsTraffic|0544": {
            $sum: "$0544.HttpsTraffic"
        },
        "HttpsTraffic|0545": {
            $sum: "$0545.HttpsTraffic"
        },
        "HttpsTraffic|0546": {
            $sum: "$0546.HttpsTraffic"
        },
        "HttpsTraffic|0547": {
            $sum: "$0547.HttpsTraffic"
        },
        "HttpsTraffic|0548": {
            $sum: "$0548.HttpsTraffic"
        },
        "HttpsTraffic|0549": {
            $sum: "$0549.HttpsTraffic"
        },
        "HttpsTraffic|0550": {
            $sum: "$0550.HttpsTraffic"
        },
        "HttpsTraffic|0551": {
            $sum: "$0551.HttpsTraffic"
        },
        "HttpsTraffic|0552": {
            $sum: "$0552.HttpsTraffic"
        },
        "HttpsTraffic|0553": {
            $sum: "$0553.HttpsTraffic"
        },
        "HttpsTraffic|0554": {
            $sum: "$0554.HttpsTraffic"
        },
        "HttpsTraffic|0555": {
            $sum: "$0555.HttpsTraffic"
        },
        "HttpsTraffic|0556": {
            $sum: "$0556.HttpsTraffic"
        },
        "HttpsTraffic|0557": {
            $sum: "$0557.HttpsTraffic"
        },
        "HttpsTraffic|0558": {
            $sum: "$0558.HttpsTraffic"
        },
        "HttpsTraffic|0559": {
            $sum: "$0559.HttpsTraffic"
        },
        "HttpsTraffic|0600": {
            $sum: "$0600.HttpsTraffic"
        },
        "HttpsTraffic|0601": {
            $sum: "$0601.HttpsTraffic"
        },
        "HttpsTraffic|0602": {
            $sum: "$0602.HttpsTraffic"
        },
        "HttpsTraffic|0603": {
            $sum: "$0603.HttpsTraffic"
        },
        "HttpsTraffic|0604": {
            $sum: "$0604.HttpsTraffic"
        },
        "HttpsTraffic|0605": {
            $sum: "$0605.HttpsTraffic"
        },
        "HttpsTraffic|0606": {
            $sum: "$0606.HttpsTraffic"
        },
        "HttpsTraffic|0607": {
            $sum: "$0607.HttpsTraffic"
        },
        "HttpsTraffic|0608": {
            $sum: "$0608.HttpsTraffic"
        },
        "HttpsTraffic|0609": {
            $sum: "$0609.HttpsTraffic"
        },
        "HttpsTraffic|0610": {
            $sum: "$0610.HttpsTraffic"
        },
        "HttpsTraffic|0611": {
            $sum: "$0611.HttpsTraffic"
        },
        "HttpsTraffic|0612": {
            $sum: "$0612.HttpsTraffic"
        },
        "HttpsTraffic|0613": {
            $sum: "$0613.HttpsTraffic"
        },
        "HttpsTraffic|0614": {
            $sum: "$0614.HttpsTraffic"
        },
        "HttpsTraffic|0615": {
            $sum: "$0615.HttpsTraffic"
        },
        "HttpsTraffic|0616": {
            $sum: "$0616.HttpsTraffic"
        },
        "HttpsTraffic|0617": {
            $sum: "$0617.HttpsTraffic"
        },
        "HttpsTraffic|0618": {
            $sum: "$0618.HttpsTraffic"
        },
        "HttpsTraffic|0619": {
            $sum: "$0619.HttpsTraffic"
        },
        "HttpsTraffic|0620": {
            $sum: "$0620.HttpsTraffic"
        },
        "HttpsTraffic|0621": {
            $sum: "$0621.HttpsTraffic"
        },
        "HttpsTraffic|0622": {
            $sum: "$0622.HttpsTraffic"
        },
        "HttpsTraffic|0623": {
            $sum: "$0623.HttpsTraffic"
        },
        "HttpsTraffic|0624": {
            $sum: "$0624.HttpsTraffic"
        },
        "HttpsTraffic|0625": {
            $sum: "$0625.HttpsTraffic"
        },
        "HttpsTraffic|0626": {
            $sum: "$0626.HttpsTraffic"
        },
        "HttpsTraffic|0627": {
            $sum: "$0627.HttpsTraffic"
        },
        "HttpsTraffic|0628": {
            $sum: "$0628.HttpsTraffic"
        },
        "HttpsTraffic|0629": {
            $sum: "$0629.HttpsTraffic"
        },
        "HttpsTraffic|0630": {
            $sum: "$0630.HttpsTraffic"
        },
        "HttpsTraffic|0631": {
            $sum: "$0631.HttpsTraffic"
        },
        "HttpsTraffic|0632": {
            $sum: "$0632.HttpsTraffic"
        },
        "HttpsTraffic|0633": {
            $sum: "$0633.HttpsTraffic"
        },
        "HttpsTraffic|0634": {
            $sum: "$0634.HttpsTraffic"
        },
        "HttpsTraffic|0635": {
            $sum: "$0635.HttpsTraffic"
        },
        "HttpsTraffic|0636": {
            $sum: "$0636.HttpsTraffic"
        },
        "HttpsTraffic|0637": {
            $sum: "$0637.HttpsTraffic"
        },
        "HttpsTraffic|0638": {
            $sum: "$0638.HttpsTraffic"
        },
        "HttpsTraffic|0639": {
            $sum: "$0639.HttpsTraffic"
        },
        "HttpsTraffic|0640": {
            $sum: "$0640.HttpsTraffic"
        },
        "HttpsTraffic|0641": {
            $sum: "$0641.HttpsTraffic"
        },
        "HttpsTraffic|0642": {
            $sum: "$0642.HttpsTraffic"
        },
        "HttpsTraffic|0643": {
            $sum: "$0643.HttpsTraffic"
        },
        "HttpsTraffic|0644": {
            $sum: "$0644.HttpsTraffic"
        },
        "HttpsTraffic|0645": {
            $sum: "$0645.HttpsTraffic"
        },
        "HttpsTraffic|0646": {
            $sum: "$0646.HttpsTraffic"
        },
        "HttpsTraffic|0647": {
            $sum: "$0647.HttpsTraffic"
        },
        "HttpsTraffic|0648": {
            $sum: "$0648.HttpsTraffic"
        },
        "HttpsTraffic|0649": {
            $sum: "$0649.HttpsTraffic"
        },
        "HttpsTraffic|0650": {
            $sum: "$0650.HttpsTraffic"
        },
        "HttpsTraffic|0651": {
            $sum: "$0651.HttpsTraffic"
        },
        "HttpsTraffic|0652": {
            $sum: "$0652.HttpsTraffic"
        },
        "HttpsTraffic|0653": {
            $sum: "$0653.HttpsTraffic"
        },
        "HttpsTraffic|0654": {
            $sum: "$0654.HttpsTraffic"
        },
        "HttpsTraffic|0655": {
            $sum: "$0655.HttpsTraffic"
        },
        "HttpsTraffic|0656": {
            $sum: "$0656.HttpsTraffic"
        },
        "HttpsTraffic|0657": {
            $sum: "$0657.HttpsTraffic"
        },
        "HttpsTraffic|0658": {
            $sum: "$0658.HttpsTraffic"
        },
        "HttpsTraffic|0659": {
            $sum: "$0659.HttpsTraffic"
        },
        "HttpsTraffic|0700": {
            $sum: "$0700.HttpsTraffic"
        },
        "HttpsTraffic|0701": {
            $sum: "$0701.HttpsTraffic"
        },
        "HttpsTraffic|0702": {
            $sum: "$0702.HttpsTraffic"
        },
        "HttpsTraffic|0703": {
            $sum: "$0703.HttpsTraffic"
        },
        "HttpsTraffic|0704": {
            $sum: "$0704.HttpsTraffic"
        },
        "HttpsTraffic|0705": {
            $sum: "$0705.HttpsTraffic"
        },
        "HttpsTraffic|0706": {
            $sum: "$0706.HttpsTraffic"
        },
        "HttpsTraffic|0707": {
            $sum: "$0707.HttpsTraffic"
        },
        "HttpsTraffic|0708": {
            $sum: "$0708.HttpsTraffic"
        },
        "HttpsTraffic|0709": {
            $sum: "$0709.HttpsTraffic"
        },
        "HttpsTraffic|0710": {
            $sum: "$0710.HttpsTraffic"
        },
        "HttpsTraffic|0711": {
            $sum: "$0711.HttpsTraffic"
        },
        "HttpsTraffic|0712": {
            $sum: "$0712.HttpsTraffic"
        },
        "HttpsTraffic|0713": {
            $sum: "$0713.HttpsTraffic"
        },
        "HttpsTraffic|0714": {
            $sum: "$0714.HttpsTraffic"
        },
        "HttpsTraffic|0715": {
            $sum: "$0715.HttpsTraffic"
        },
        "HttpsTraffic|0716": {
            $sum: "$0716.HttpsTraffic"
        },
        "HttpsTraffic|0717": {
            $sum: "$0717.HttpsTraffic"
        },
        "HttpsTraffic|0718": {
            $sum: "$0718.HttpsTraffic"
        },
        "HttpsTraffic|0719": {
            $sum: "$0719.HttpsTraffic"
        },
        "HttpsTraffic|0720": {
            $sum: "$0720.HttpsTraffic"
        },
        "HttpsTraffic|0721": {
            $sum: "$0721.HttpsTraffic"
        },
        "HttpsTraffic|0722": {
            $sum: "$0722.HttpsTraffic"
        },
        "HttpsTraffic|0723": {
            $sum: "$0723.HttpsTraffic"
        },
        "HttpsTraffic|0724": {
            $sum: "$0724.HttpsTraffic"
        },
        "HttpsTraffic|0725": {
            $sum: "$0725.HttpsTraffic"
        },
        "HttpsTraffic|0726": {
            $sum: "$0726.HttpsTraffic"
        },
        "HttpsTraffic|0727": {
            $sum: "$0727.HttpsTraffic"
        },
        "HttpsTraffic|0728": {
            $sum: "$0728.HttpsTraffic"
        },
        "HttpsTraffic|0729": {
            $sum: "$0729.HttpsTraffic"
        },
        "HttpsTraffic|0730": {
            $sum: "$0730.HttpsTraffic"
        },
        "HttpsTraffic|0731": {
            $sum: "$0731.HttpsTraffic"
        },
        "HttpsTraffic|0732": {
            $sum: "$0732.HttpsTraffic"
        },
        "HttpsTraffic|0733": {
            $sum: "$0733.HttpsTraffic"
        },
        "HttpsTraffic|0734": {
            $sum: "$0734.HttpsTraffic"
        },
        "HttpsTraffic|0735": {
            $sum: "$0735.HttpsTraffic"
        },
        "HttpsTraffic|0736": {
            $sum: "$0736.HttpsTraffic"
        },
        "HttpsTraffic|0737": {
            $sum: "$0737.HttpsTraffic"
        },
        "HttpsTraffic|0738": {
            $sum: "$0738.HttpsTraffic"
        },
        "HttpsTraffic|0739": {
            $sum: "$0739.HttpsTraffic"
        },
        "HttpsTraffic|0740": {
            $sum: "$0740.HttpsTraffic"
        },
        "HttpsTraffic|0741": {
            $sum: "$0741.HttpsTraffic"
        },
        "HttpsTraffic|0742": {
            $sum: "$0742.HttpsTraffic"
        },
        "HttpsTraffic|0743": {
            $sum: "$0743.HttpsTraffic"
        },
        "HttpsTraffic|0744": {
            $sum: "$0744.HttpsTraffic"
        },
        "HttpsTraffic|0745": {
            $sum: "$0745.HttpsTraffic"
        },
        "HttpsTraffic|0746": {
            $sum: "$0746.HttpsTraffic"
        },
        "HttpsTraffic|0747": {
            $sum: "$0747.HttpsTraffic"
        },
        "HttpsTraffic|0748": {
            $sum: "$0748.HttpsTraffic"
        },
        "HttpsTraffic|0749": {
            $sum: "$0749.HttpsTraffic"
        },
        "HttpsTraffic|0750": {
            $sum: "$0750.HttpsTraffic"
        },
        "HttpsTraffic|0751": {
            $sum: "$0751.HttpsTraffic"
        },
        "HttpsTraffic|0752": {
            $sum: "$0752.HttpsTraffic"
        },
        "HttpsTraffic|0753": {
            $sum: "$0753.HttpsTraffic"
        },
        "HttpsTraffic|0754": {
            $sum: "$0754.HttpsTraffic"
        },
        "HttpsTraffic|0755": {
            $sum: "$0755.HttpsTraffic"
        },
        "HttpsTraffic|0756": {
            $sum: "$0756.HttpsTraffic"
        },
        "HttpsTraffic|0757": {
            $sum: "$0757.HttpsTraffic"
        },
        "HttpsTraffic|0758": {
            $sum: "$0758.HttpsTraffic"
        },
        "HttpsTraffic|0759": {
            $sum: "$0759.HttpsTraffic"
        },
        "HttpsTraffic|0800": {
            $sum: "$0800.HttpsTraffic"
        },
        "HttpsTraffic|0801": {
            $sum: "$0801.HttpsTraffic"
        },
        "HttpsTraffic|0802": {
            $sum: "$0802.HttpsTraffic"
        },
        "HttpsTraffic|0803": {
            $sum: "$0803.HttpsTraffic"
        },
        "HttpsTraffic|0804": {
            $sum: "$0804.HttpsTraffic"
        },
        "HttpsTraffic|0805": {
            $sum: "$0805.HttpsTraffic"
        },
        "HttpsTraffic|0806": {
            $sum: "$0806.HttpsTraffic"
        },
        "HttpsTraffic|0807": {
            $sum: "$0807.HttpsTraffic"
        },
        "HttpsTraffic|0808": {
            $sum: "$0808.HttpsTraffic"
        },
        "HttpsTraffic|0809": {
            $sum: "$0809.HttpsTraffic"
        },
        "HttpsTraffic|0810": {
            $sum: "$0810.HttpsTraffic"
        },
        "HttpsTraffic|0811": {
            $sum: "$0811.HttpsTraffic"
        },
        "HttpsTraffic|0812": {
            $sum: "$0812.HttpsTraffic"
        },
        "HttpsTraffic|0813": {
            $sum: "$0813.HttpsTraffic"
        },
        "HttpsTraffic|0814": {
            $sum: "$0814.HttpsTraffic"
        },
        "HttpsTraffic|0815": {
            $sum: "$0815.HttpsTraffic"
        },
        "HttpsTraffic|0816": {
            $sum: "$0816.HttpsTraffic"
        },
        "HttpsTraffic|0817": {
            $sum: "$0817.HttpsTraffic"
        },
        "HttpsTraffic|0818": {
            $sum: "$0818.HttpsTraffic"
        },
        "HttpsTraffic|0819": {
            $sum: "$0819.HttpsTraffic"
        },
        "HttpsTraffic|0820": {
            $sum: "$0820.HttpsTraffic"
        },
        "HttpsTraffic|0821": {
            $sum: "$0821.HttpsTraffic"
        },
        "HttpsTraffic|0822": {
            $sum: "$0822.HttpsTraffic"
        },
        "HttpsTraffic|0823": {
            $sum: "$0823.HttpsTraffic"
        },
        "HttpsTraffic|0824": {
            $sum: "$0824.HttpsTraffic"
        },
        "HttpsTraffic|0825": {
            $sum: "$0825.HttpsTraffic"
        },
        "HttpsTraffic|0826": {
            $sum: "$0826.HttpsTraffic"
        },
        "HttpsTraffic|0827": {
            $sum: "$0827.HttpsTraffic"
        },
        "HttpsTraffic|0828": {
            $sum: "$0828.HttpsTraffic"
        },
        "HttpsTraffic|0829": {
            $sum: "$0829.HttpsTraffic"
        },
        "HttpsTraffic|0830": {
            $sum: "$0830.HttpsTraffic"
        },
        "HttpsTraffic|0831": {
            $sum: "$0831.HttpsTraffic"
        },
        "HttpsTraffic|0832": {
            $sum: "$0832.HttpsTraffic"
        },
        "HttpsTraffic|0833": {
            $sum: "$0833.HttpsTraffic"
        },
        "HttpsTraffic|0834": {
            $sum: "$0834.HttpsTraffic"
        },
        "HttpsTraffic|0835": {
            $sum: "$0835.HttpsTraffic"
        },
        "HttpsTraffic|0836": {
            $sum: "$0836.HttpsTraffic"
        },
        "HttpsTraffic|0837": {
            $sum: "$0837.HttpsTraffic"
        },
        "HttpsTraffic|0838": {
            $sum: "$0838.HttpsTraffic"
        },
        "HttpsTraffic|0839": {
            $sum: "$0839.HttpsTraffic"
        },
        "HttpsTraffic|0840": {
            $sum: "$0840.HttpsTraffic"
        },
        "HttpsTraffic|0841": {
            $sum: "$0841.HttpsTraffic"
        },
        "HttpsTraffic|0842": {
            $sum: "$0842.HttpsTraffic"
        },
        "HttpsTraffic|0843": {
            $sum: "$0843.HttpsTraffic"
        },
        "HttpsTraffic|0844": {
            $sum: "$0844.HttpsTraffic"
        },
        "HttpsTraffic|0845": {
            $sum: "$0845.HttpsTraffic"
        },
        "HttpsTraffic|0846": {
            $sum: "$0846.HttpsTraffic"
        },
        "HttpsTraffic|0847": {
            $sum: "$0847.HttpsTraffic"
        },
        "HttpsTraffic|0848": {
            $sum: "$0848.HttpsTraffic"
        },
        "HttpsTraffic|0849": {
            $sum: "$0849.HttpsTraffic"
        },
        "HttpsTraffic|0850": {
            $sum: "$0850.HttpsTraffic"
        },
        "HttpsTraffic|0851": {
            $sum: "$0851.HttpsTraffic"
        },
        "HttpsTraffic|0852": {
            $sum: "$0852.HttpsTraffic"
        },
        "HttpsTraffic|0853": {
            $sum: "$0853.HttpsTraffic"
        },
        "HttpsTraffic|0854": {
            $sum: "$0854.HttpsTraffic"
        },
        "HttpsTraffic|0855": {
            $sum: "$0855.HttpsTraffic"
        },
        "HttpsTraffic|0856": {
            $sum: "$0856.HttpsTraffic"
        },
        "HttpsTraffic|0857": {
            $sum: "$0857.HttpsTraffic"
        },
        "HttpsTraffic|0858": {
            $sum: "$0858.HttpsTraffic"
        },
        "HttpsTraffic|0859": {
            $sum: "$0859.HttpsTraffic"
        },
        "HttpsTraffic|0900": {
            $sum: "$0900.HttpsTraffic"
        },
        "HttpsTraffic|0901": {
            $sum: "$0901.HttpsTraffic"
        },
        "HttpsTraffic|0902": {
            $sum: "$0902.HttpsTraffic"
        },
        "HttpsTraffic|0903": {
            $sum: "$0903.HttpsTraffic"
        },
        "HttpsTraffic|0904": {
            $sum: "$0904.HttpsTraffic"
        },
        "HttpsTraffic|0905": {
            $sum: "$0905.HttpsTraffic"
        },
        "HttpsTraffic|0906": {
            $sum: "$0906.HttpsTraffic"
        },
        "HttpsTraffic|0907": {
            $sum: "$0907.HttpsTraffic"
        },
        "HttpsTraffic|0908": {
            $sum: "$0908.HttpsTraffic"
        },
        "HttpsTraffic|0909": {
            $sum: "$0909.HttpsTraffic"
        },
        "HttpsTraffic|0910": {
            $sum: "$0910.HttpsTraffic"
        },
        "HttpsTraffic|0911": {
            $sum: "$0911.HttpsTraffic"
        },
        "HttpsTraffic|0912": {
            $sum: "$0912.HttpsTraffic"
        },
        "HttpsTraffic|0913": {
            $sum: "$0913.HttpsTraffic"
        },
        "HttpsTraffic|0914": {
            $sum: "$0914.HttpsTraffic"
        },
        "HttpsTraffic|0915": {
            $sum: "$0915.HttpsTraffic"
        },
        "HttpsTraffic|0916": {
            $sum: "$0916.HttpsTraffic"
        },
        "HttpsTraffic|0917": {
            $sum: "$0917.HttpsTraffic"
        },
        "HttpsTraffic|0918": {
            $sum: "$0918.HttpsTraffic"
        },
        "HttpsTraffic|0919": {
            $sum: "$0919.HttpsTraffic"
        },
        "HttpsTraffic|0920": {
            $sum: "$0920.HttpsTraffic"
        },
        "HttpsTraffic|0921": {
            $sum: "$0921.HttpsTraffic"
        },
        "HttpsTraffic|0922": {
            $sum: "$0922.HttpsTraffic"
        },
        "HttpsTraffic|0923": {
            $sum: "$0923.HttpsTraffic"
        },
        "HttpsTraffic|0924": {
            $sum: "$0924.HttpsTraffic"
        },
        "HttpsTraffic|0925": {
            $sum: "$0925.HttpsTraffic"
        },
        "HttpsTraffic|0926": {
            $sum: "$0926.HttpsTraffic"
        },
        "HttpsTraffic|0927": {
            $sum: "$0927.HttpsTraffic"
        },
        "HttpsTraffic|0928": {
            $sum: "$0928.HttpsTraffic"
        },
        "HttpsTraffic|0929": {
            $sum: "$0929.HttpsTraffic"
        },
        "HttpsTraffic|0930": {
            $sum: "$0930.HttpsTraffic"
        },
        "HttpsTraffic|0931": {
            $sum: "$0931.HttpsTraffic"
        },
        "HttpsTraffic|0932": {
            $sum: "$0932.HttpsTraffic"
        },
        "HttpsTraffic|0933": {
            $sum: "$0933.HttpsTraffic"
        },
        "HttpsTraffic|0934": {
            $sum: "$0934.HttpsTraffic"
        },
        "HttpsTraffic|0935": {
            $sum: "$0935.HttpsTraffic"
        },
        "HttpsTraffic|0936": {
            $sum: "$0936.HttpsTraffic"
        },
        "HttpsTraffic|0937": {
            $sum: "$0937.HttpsTraffic"
        },
        "HttpsTraffic|0938": {
            $sum: "$0938.HttpsTraffic"
        },
        "HttpsTraffic|0939": {
            $sum: "$0939.HttpsTraffic"
        },
        "HttpsTraffic|0940": {
            $sum: "$0940.HttpsTraffic"
        },
        "HttpsTraffic|0941": {
            $sum: "$0941.HttpsTraffic"
        },
        "HttpsTraffic|0942": {
            $sum: "$0942.HttpsTraffic"
        },
        "HttpsTraffic|0943": {
            $sum: "$0943.HttpsTraffic"
        },
        "HttpsTraffic|0944": {
            $sum: "$0944.HttpsTraffic"
        },
        "HttpsTraffic|0945": {
            $sum: "$0945.HttpsTraffic"
        },
        "HttpsTraffic|0946": {
            $sum: "$0946.HttpsTraffic"
        },
        "HttpsTraffic|0947": {
            $sum: "$0947.HttpsTraffic"
        },
        "HttpsTraffic|0948": {
            $sum: "$0948.HttpsTraffic"
        },
        "HttpsTraffic|0949": {
            $sum: "$0949.HttpsTraffic"
        },
        "HttpsTraffic|0950": {
            $sum: "$0950.HttpsTraffic"
        },
        "HttpsTraffic|0951": {
            $sum: "$0951.HttpsTraffic"
        },
        "HttpsTraffic|0952": {
            $sum: "$0952.HttpsTraffic"
        },
        "HttpsTraffic|0953": {
            $sum: "$0953.HttpsTraffic"
        },
        "HttpsTraffic|0954": {
            $sum: "$0954.HttpsTraffic"
        },
        "HttpsTraffic|0955": {
            $sum: "$0955.HttpsTraffic"
        },
        "HttpsTraffic|0956": {
            $sum: "$0956.HttpsTraffic"
        },
        "HttpsTraffic|0957": {
            $sum: "$0957.HttpsTraffic"
        },
        "HttpsTraffic|0958": {
            $sum: "$0958.HttpsTraffic"
        },
        "HttpsTraffic|0959": {
            $sum: "$0959.HttpsTraffic"
        },
        "HttpsTraffic|1000": {
            $sum: "$1000.HttpsTraffic"
        },
        "HttpsTraffic|1001": {
            $sum: "$1001.HttpsTraffic"
        },
        "HttpsTraffic|1002": {
            $sum: "$1002.HttpsTraffic"
        },
        "HttpsTraffic|1003": {
            $sum: "$1003.HttpsTraffic"
        },
        "HttpsTraffic|1004": {
            $sum: "$1004.HttpsTraffic"
        },
        "HttpsTraffic|1005": {
            $sum: "$1005.HttpsTraffic"
        },
        "HttpsTraffic|1006": {
            $sum: "$1006.HttpsTraffic"
        },
        "HttpsTraffic|1007": {
            $sum: "$1007.HttpsTraffic"
        },
        "HttpsTraffic|1008": {
            $sum: "$1008.HttpsTraffic"
        },
        "HttpsTraffic|1009": {
            $sum: "$1009.HttpsTraffic"
        },
        "HttpsTraffic|1010": {
            $sum: "$1010.HttpsTraffic"
        },
        "HttpsTraffic|1011": {
            $sum: "$1011.HttpsTraffic"
        },
        "HttpsTraffic|1012": {
            $sum: "$1012.HttpsTraffic"
        },
        "HttpsTraffic|1013": {
            $sum: "$1013.HttpsTraffic"
        },
        "HttpsTraffic|1014": {
            $sum: "$1014.HttpsTraffic"
        },
        "HttpsTraffic|1015": {
            $sum: "$1015.HttpsTraffic"
        },
        "HttpsTraffic|1016": {
            $sum: "$1016.HttpsTraffic"
        },
        "HttpsTraffic|1017": {
            $sum: "$1017.HttpsTraffic"
        },
        "HttpsTraffic|1018": {
            $sum: "$1018.HttpsTraffic"
        },
        "HttpsTraffic|1019": {
            $sum: "$1019.HttpsTraffic"
        },
        "HttpsTraffic|1020": {
            $sum: "$1020.HttpsTraffic"
        },
        "HttpsTraffic|1021": {
            $sum: "$1021.HttpsTraffic"
        },
        "HttpsTraffic|1022": {
            $sum: "$1022.HttpsTraffic"
        },
        "HttpsTraffic|1023": {
            $sum: "$1023.HttpsTraffic"
        },
        "HttpsTraffic|1024": {
            $sum: "$1024.HttpsTraffic"
        },
        "HttpsTraffic|1025": {
            $sum: "$1025.HttpsTraffic"
        },
        "HttpsTraffic|1026": {
            $sum: "$1026.HttpsTraffic"
        },
        "HttpsTraffic|1027": {
            $sum: "$1027.HttpsTraffic"
        },
        "HttpsTraffic|1028": {
            $sum: "$1028.HttpsTraffic"
        },
        "HttpsTraffic|1029": {
            $sum: "$1029.HttpsTraffic"
        },
        "HttpsTraffic|1030": {
            $sum: "$1030.HttpsTraffic"
        },
        "HttpsTraffic|1031": {
            $sum: "$1031.HttpsTraffic"
        },
        "HttpsTraffic|1032": {
            $sum: "$1032.HttpsTraffic"
        },
        "HttpsTraffic|1033": {
            $sum: "$1033.HttpsTraffic"
        },
        "HttpsTraffic|1034": {
            $sum: "$1034.HttpsTraffic"
        },
        "HttpsTraffic|1035": {
            $sum: "$1035.HttpsTraffic"
        },
        "HttpsTraffic|1036": {
            $sum: "$1036.HttpsTraffic"
        },
        "HttpsTraffic|1037": {
            $sum: "$1037.HttpsTraffic"
        },
        "HttpsTraffic|1038": {
            $sum: "$1038.HttpsTraffic"
        },
        "HttpsTraffic|1039": {
            $sum: "$1039.HttpsTraffic"
        },
        "HttpsTraffic|1040": {
            $sum: "$1040.HttpsTraffic"
        },
        "HttpsTraffic|1041": {
            $sum: "$1041.HttpsTraffic"
        },
        "HttpsTraffic|1042": {
            $sum: "$1042.HttpsTraffic"
        },
        "HttpsTraffic|1043": {
            $sum: "$1043.HttpsTraffic"
        },
        "HttpsTraffic|1044": {
            $sum: "$1044.HttpsTraffic"
        },
        "HttpsTraffic|1045": {
            $sum: "$1045.HttpsTraffic"
        },
        "HttpsTraffic|1046": {
            $sum: "$1046.HttpsTraffic"
        },
        "HttpsTraffic|1047": {
            $sum: "$1047.HttpsTraffic"
        },
        "HttpsTraffic|1048": {
            $sum: "$1048.HttpsTraffic"
        },
        "HttpsTraffic|1049": {
            $sum: "$1049.HttpsTraffic"
        },
        "HttpsTraffic|1050": {
            $sum: "$1050.HttpsTraffic"
        },
        "HttpsTraffic|1051": {
            $sum: "$1051.HttpsTraffic"
        },
        "HttpsTraffic|1052": {
            $sum: "$1052.HttpsTraffic"
        },
        "HttpsTraffic|1053": {
            $sum: "$1053.HttpsTraffic"
        },
        "HttpsTraffic|1054": {
            $sum: "$1054.HttpsTraffic"
        },
        "HttpsTraffic|1055": {
            $sum: "$1055.HttpsTraffic"
        },
        "HttpsTraffic|1056": {
            $sum: "$1056.HttpsTraffic"
        },
        "HttpsTraffic|1057": {
            $sum: "$1057.HttpsTraffic"
        },
        "HttpsTraffic|1058": {
            $sum: "$1058.HttpsTraffic"
        },
        "HttpsTraffic|1059": {
            $sum: "$1059.HttpsTraffic"
        },
        "HttpsTraffic|1100": {
            $sum: "$1100.HttpsTraffic"
        },
        "HttpsTraffic|1101": {
            $sum: "$1101.HttpsTraffic"
        },
        "HttpsTraffic|1102": {
            $sum: "$1102.HttpsTraffic"
        },
        "HttpsTraffic|1103": {
            $sum: "$1103.HttpsTraffic"
        },
        "HttpsTraffic|1104": {
            $sum: "$1104.HttpsTraffic"
        },
        "HttpsTraffic|1105": {
            $sum: "$1105.HttpsTraffic"
        },
        "HttpsTraffic|1106": {
            $sum: "$1106.HttpsTraffic"
        },
        "HttpsTraffic|1107": {
            $sum: "$1107.HttpsTraffic"
        },
        "HttpsTraffic|1108": {
            $sum: "$1108.HttpsTraffic"
        },
        "HttpsTraffic|1109": {
            $sum: "$1109.HttpsTraffic"
        },
        "HttpsTraffic|1110": {
            $sum: "$1110.HttpsTraffic"
        },
        "HttpsTraffic|1111": {
            $sum: "$1111.HttpsTraffic"
        },
        "HttpsTraffic|1112": {
            $sum: "$1112.HttpsTraffic"
        },
        "HttpsTraffic|1113": {
            $sum: "$1113.HttpsTraffic"
        },
        "HttpsTraffic|1114": {
            $sum: "$1114.HttpsTraffic"
        },
        "HttpsTraffic|1115": {
            $sum: "$1115.HttpsTraffic"
        },
        "HttpsTraffic|1116": {
            $sum: "$1116.HttpsTraffic"
        },
        "HttpsTraffic|1117": {
            $sum: "$1117.HttpsTraffic"
        },
        "HttpsTraffic|1118": {
            $sum: "$1118.HttpsTraffic"
        },
        "HttpsTraffic|1119": {
            $sum: "$1119.HttpsTraffic"
        },
        "HttpsTraffic|1120": {
            $sum: "$1120.HttpsTraffic"
        },
        "HttpsTraffic|1121": {
            $sum: "$1121.HttpsTraffic"
        },
        "HttpsTraffic|1122": {
            $sum: "$1122.HttpsTraffic"
        },
        "HttpsTraffic|1123": {
            $sum: "$1123.HttpsTraffic"
        },
        "HttpsTraffic|1124": {
            $sum: "$1124.HttpsTraffic"
        },
        "HttpsTraffic|1125": {
            $sum: "$1125.HttpsTraffic"
        },
        "HttpsTraffic|1126": {
            $sum: "$1126.HttpsTraffic"
        },
        "HttpsTraffic|1127": {
            $sum: "$1127.HttpsTraffic"
        },
        "HttpsTraffic|1128": {
            $sum: "$1128.HttpsTraffic"
        },
        "HttpsTraffic|1129": {
            $sum: "$1129.HttpsTraffic"
        },
        "HttpsTraffic|1130": {
            $sum: "$1130.HttpsTraffic"
        },
        "HttpsTraffic|1131": {
            $sum: "$1131.HttpsTraffic"
        },
        "HttpsTraffic|1132": {
            $sum: "$1132.HttpsTraffic"
        },
        "HttpsTraffic|1133": {
            $sum: "$1133.HttpsTraffic"
        },
        "HttpsTraffic|1134": {
            $sum: "$1134.HttpsTraffic"
        },
        "HttpsTraffic|1135": {
            $sum: "$1135.HttpsTraffic"
        },
        "HttpsTraffic|1136": {
            $sum: "$1136.HttpsTraffic"
        },
        "HttpsTraffic|1137": {
            $sum: "$1137.HttpsTraffic"
        },
        "HttpsTraffic|1138": {
            $sum: "$1138.HttpsTraffic"
        },
        "HttpsTraffic|1139": {
            $sum: "$1139.HttpsTraffic"
        },
        "HttpsTraffic|1140": {
            $sum: "$1140.HttpsTraffic"
        },
        "HttpsTraffic|1141": {
            $sum: "$1141.HttpsTraffic"
        },
        "HttpsTraffic|1142": {
            $sum: "$1142.HttpsTraffic"
        },
        "HttpsTraffic|1143": {
            $sum: "$1143.HttpsTraffic"
        },
        "HttpsTraffic|1144": {
            $sum: "$1144.HttpsTraffic"
        },
        "HttpsTraffic|1145": {
            $sum: "$1145.HttpsTraffic"
        },
        "HttpsTraffic|1146": {
            $sum: "$1146.HttpsTraffic"
        },
        "HttpsTraffic|1147": {
            $sum: "$1147.HttpsTraffic"
        },
        "HttpsTraffic|1148": {
            $sum: "$1148.HttpsTraffic"
        },
        "HttpsTraffic|1149": {
            $sum: "$1149.HttpsTraffic"
        },
        "HttpsTraffic|1150": {
            $sum: "$1150.HttpsTraffic"
        },
        "HttpsTraffic|1151": {
            $sum: "$1151.HttpsTraffic"
        },
        "HttpsTraffic|1152": {
            $sum: "$1152.HttpsTraffic"
        },
        "HttpsTraffic|1153": {
            $sum: "$1153.HttpsTraffic"
        },
        "HttpsTraffic|1154": {
            $sum: "$1154.HttpsTraffic"
        },
        "HttpsTraffic|1155": {
            $sum: "$1155.HttpsTraffic"
        },
        "HttpsTraffic|1156": {
            $sum: "$1156.HttpsTraffic"
        },
        "HttpsTraffic|1157": {
            $sum: "$1157.HttpsTraffic"
        },
        "HttpsTraffic|1158": {
            $sum: "$1158.HttpsTraffic"
        },
        "HttpsTraffic|1159": {
            $sum: "$1159.HttpsTraffic"
        },
        "HttpsTraffic|1200": {
            $sum: "$1200.HttpsTraffic"
        },
        "HttpsTraffic|1201": {
            $sum: "$1201.HttpsTraffic"
        },
        "HttpsTraffic|1202": {
            $sum: "$1202.HttpsTraffic"
        },
        "HttpsTraffic|1203": {
            $sum: "$1203.HttpsTraffic"
        },
        "HttpsTraffic|1204": {
            $sum: "$1204.HttpsTraffic"
        },
        "HttpsTraffic|1205": {
            $sum: "$1205.HttpsTraffic"
        },
        "HttpsTraffic|1206": {
            $sum: "$1206.HttpsTraffic"
        },
        "HttpsTraffic|1207": {
            $sum: "$1207.HttpsTraffic"
        },
        "HttpsTraffic|1208": {
            $sum: "$1208.HttpsTraffic"
        },
        "HttpsTraffic|1209": {
            $sum: "$1209.HttpsTraffic"
        },
        "HttpsTraffic|1210": {
            $sum: "$1210.HttpsTraffic"
        },
        "HttpsTraffic|1211": {
            $sum: "$1211.HttpsTraffic"
        },
        "HttpsTraffic|1212": {
            $sum: "$1212.HttpsTraffic"
        },
        "HttpsTraffic|1213": {
            $sum: "$1213.HttpsTraffic"
        },
        "HttpsTraffic|1214": {
            $sum: "$1214.HttpsTraffic"
        },
        "HttpsTraffic|1215": {
            $sum: "$1215.HttpsTraffic"
        },
        "HttpsTraffic|1216": {
            $sum: "$1216.HttpsTraffic"
        },
        "HttpsTraffic|1217": {
            $sum: "$1217.HttpsTraffic"
        },
        "HttpsTraffic|1218": {
            $sum: "$1218.HttpsTraffic"
        },
        "HttpsTraffic|1219": {
            $sum: "$1219.HttpsTraffic"
        },
        "HttpsTraffic|1220": {
            $sum: "$1220.HttpsTraffic"
        },
        "HttpsTraffic|1221": {
            $sum: "$1221.HttpsTraffic"
        },
        "HttpsTraffic|1222": {
            $sum: "$1222.HttpsTraffic"
        },
        "HttpsTraffic|1223": {
            $sum: "$1223.HttpsTraffic"
        },
        "HttpsTraffic|1224": {
            $sum: "$1224.HttpsTraffic"
        },
        "HttpsTraffic|1225": {
            $sum: "$1225.HttpsTraffic"
        },
        "HttpsTraffic|1226": {
            $sum: "$1226.HttpsTraffic"
        },
        "HttpsTraffic|1227": {
            $sum: "$1227.HttpsTraffic"
        },
        "HttpsTraffic|1228": {
            $sum: "$1228.HttpsTraffic"
        },
        "HttpsTraffic|1229": {
            $sum: "$1229.HttpsTraffic"
        },
        "HttpsTraffic|1230": {
            $sum: "$1230.HttpsTraffic"
        },
        "HttpsTraffic|1231": {
            $sum: "$1231.HttpsTraffic"
        },
        "HttpsTraffic|1232": {
            $sum: "$1232.HttpsTraffic"
        },
        "HttpsTraffic|1233": {
            $sum: "$1233.HttpsTraffic"
        },
        "HttpsTraffic|1234": {
            $sum: "$1234.HttpsTraffic"
        },
        "HttpsTraffic|1235": {
            $sum: "$1235.HttpsTraffic"
        },
        "HttpsTraffic|1236": {
            $sum: "$1236.HttpsTraffic"
        },
        "HttpsTraffic|1237": {
            $sum: "$1237.HttpsTraffic"
        },
        "HttpsTraffic|1238": {
            $sum: "$1238.HttpsTraffic"
        },
        "HttpsTraffic|1239": {
            $sum: "$1239.HttpsTraffic"
        },
        "HttpsTraffic|1240": {
            $sum: "$1240.HttpsTraffic"
        },
        "HttpsTraffic|1241": {
            $sum: "$1241.HttpsTraffic"
        },
        "HttpsTraffic|1242": {
            $sum: "$1242.HttpsTraffic"
        },
        "HttpsTraffic|1243": {
            $sum: "$1243.HttpsTraffic"
        },
        "HttpsTraffic|1244": {
            $sum: "$1244.HttpsTraffic"
        },
        "HttpsTraffic|1245": {
            $sum: "$1245.HttpsTraffic"
        },
        "HttpsTraffic|1246": {
            $sum: "$1246.HttpsTraffic"
        },
        "HttpsTraffic|1247": {
            $sum: "$1247.HttpsTraffic"
        },
        "HttpsTraffic|1248": {
            $sum: "$1248.HttpsTraffic"
        },
        "HttpsTraffic|1249": {
            $sum: "$1249.HttpsTraffic"
        },
        "HttpsTraffic|1250": {
            $sum: "$1250.HttpsTraffic"
        },
        "HttpsTraffic|1251": {
            $sum: "$1251.HttpsTraffic"
        },
        "HttpsTraffic|1252": {
            $sum: "$1252.HttpsTraffic"
        },
        "HttpsTraffic|1253": {
            $sum: "$1253.HttpsTraffic"
        },
        "HttpsTraffic|1254": {
            $sum: "$1254.HttpsTraffic"
        },
        "HttpsTraffic|1255": {
            $sum: "$1255.HttpsTraffic"
        },
        "HttpsTraffic|1256": {
            $sum: "$1256.HttpsTraffic"
        },
        "HttpsTraffic|1257": {
            $sum: "$1257.HttpsTraffic"
        },
        "HttpsTraffic|1258": {
            $sum: "$1258.HttpsTraffic"
        },
        "HttpsTraffic|1259": {
            $sum: "$1259.HttpsTraffic"
        },
        "HttpsTraffic|1300": {
            $sum: "$1300.HttpsTraffic"
        },
        "HttpsTraffic|1301": {
            $sum: "$1301.HttpsTraffic"
        },
        "HttpsTraffic|1302": {
            $sum: "$1302.HttpsTraffic"
        },
        "HttpsTraffic|1303": {
            $sum: "$1303.HttpsTraffic"
        },
        "HttpsTraffic|1304": {
            $sum: "$1304.HttpsTraffic"
        },
        "HttpsTraffic|1305": {
            $sum: "$1305.HttpsTraffic"
        },
        "HttpsTraffic|1306": {
            $sum: "$1306.HttpsTraffic"
        },
        "HttpsTraffic|1307": {
            $sum: "$1307.HttpsTraffic"
        },
        "HttpsTraffic|1308": {
            $sum: "$1308.HttpsTraffic"
        },
        "HttpsTraffic|1309": {
            $sum: "$1309.HttpsTraffic"
        },
        "HttpsTraffic|1310": {
            $sum: "$1310.HttpsTraffic"
        },
        "HttpsTraffic|1311": {
            $sum: "$1311.HttpsTraffic"
        },
        "HttpsTraffic|1312": {
            $sum: "$1312.HttpsTraffic"
        },
        "HttpsTraffic|1313": {
            $sum: "$1313.HttpsTraffic"
        },
        "HttpsTraffic|1314": {
            $sum: "$1314.HttpsTraffic"
        },
        "HttpsTraffic|1315": {
            $sum: "$1315.HttpsTraffic"
        },
        "HttpsTraffic|1316": {
            $sum: "$1316.HttpsTraffic"
        },
        "HttpsTraffic|1317": {
            $sum: "$1317.HttpsTraffic"
        },
        "HttpsTraffic|1318": {
            $sum: "$1318.HttpsTraffic"
        },
        "HttpsTraffic|1319": {
            $sum: "$1319.HttpsTraffic"
        },
        "HttpsTraffic|1320": {
            $sum: "$1320.HttpsTraffic"
        },
        "HttpsTraffic|1321": {
            $sum: "$1321.HttpsTraffic"
        },
        "HttpsTraffic|1322": {
            $sum: "$1322.HttpsTraffic"
        },
        "HttpsTraffic|1323": {
            $sum: "$1323.HttpsTraffic"
        },
        "HttpsTraffic|1324": {
            $sum: "$1324.HttpsTraffic"
        },
        "HttpsTraffic|1325": {
            $sum: "$1325.HttpsTraffic"
        },
        "HttpsTraffic|1326": {
            $sum: "$1326.HttpsTraffic"
        },
        "HttpsTraffic|1327": {
            $sum: "$1327.HttpsTraffic"
        },
        "HttpsTraffic|1328": {
            $sum: "$1328.HttpsTraffic"
        },
        "HttpsTraffic|1329": {
            $sum: "$1329.HttpsTraffic"
        },
        "HttpsTraffic|1330": {
            $sum: "$1330.HttpsTraffic"
        },
        "HttpsTraffic|1331": {
            $sum: "$1331.HttpsTraffic"
        },
        "HttpsTraffic|1332": {
            $sum: "$1332.HttpsTraffic"
        },
        "HttpsTraffic|1333": {
            $sum: "$1333.HttpsTraffic"
        },
        "HttpsTraffic|1334": {
            $sum: "$1334.HttpsTraffic"
        },
        "HttpsTraffic|1335": {
            $sum: "$1335.HttpsTraffic"
        },
        "HttpsTraffic|1336": {
            $sum: "$1336.HttpsTraffic"
        },
        "HttpsTraffic|1337": {
            $sum: "$1337.HttpsTraffic"
        },
        "HttpsTraffic|1338": {
            $sum: "$1338.HttpsTraffic"
        },
        "HttpsTraffic|1339": {
            $sum: "$1339.HttpsTraffic"
        },
        "HttpsTraffic|1340": {
            $sum: "$1340.HttpsTraffic"
        },
        "HttpsTraffic|1341": {
            $sum: "$1341.HttpsTraffic"
        },
        "HttpsTraffic|1342": {
            $sum: "$1342.HttpsTraffic"
        },
        "HttpsTraffic|1343": {
            $sum: "$1343.HttpsTraffic"
        },
        "HttpsTraffic|1344": {
            $sum: "$1344.HttpsTraffic"
        },
        "HttpsTraffic|1345": {
            $sum: "$1345.HttpsTraffic"
        },
        "HttpsTraffic|1346": {
            $sum: "$1346.HttpsTraffic"
        },
        "HttpsTraffic|1347": {
            $sum: "$1347.HttpsTraffic"
        },
        "HttpsTraffic|1348": {
            $sum: "$1348.HttpsTraffic"
        },
        "HttpsTraffic|1349": {
            $sum: "$1349.HttpsTraffic"
        },
        "HttpsTraffic|1350": {
            $sum: "$1350.HttpsTraffic"
        },
        "HttpsTraffic|1351": {
            $sum: "$1351.HttpsTraffic"
        },
        "HttpsTraffic|1352": {
            $sum: "$1352.HttpsTraffic"
        },
        "HttpsTraffic|1353": {
            $sum: "$1353.HttpsTraffic"
        },
        "HttpsTraffic|1354": {
            $sum: "$1354.HttpsTraffic"
        },
        "HttpsTraffic|1355": {
            $sum: "$1355.HttpsTraffic"
        },
        "HttpsTraffic|1356": {
            $sum: "$1356.HttpsTraffic"
        },
        "HttpsTraffic|1357": {
            $sum: "$1357.HttpsTraffic"
        },
        "HttpsTraffic|1358": {
            $sum: "$1358.HttpsTraffic"
        },
        "HttpsTraffic|1359": {
            $sum: "$1359.HttpsTraffic"
        },
        "HttpsTraffic|1400": {
            $sum: "$1400.HttpsTraffic"
        },
        "HttpsTraffic|1401": {
            $sum: "$1401.HttpsTraffic"
        },
        "HttpsTraffic|1402": {
            $sum: "$1402.HttpsTraffic"
        },
        "HttpsTraffic|1403": {
            $sum: "$1403.HttpsTraffic"
        },
        "HttpsTraffic|1404": {
            $sum: "$1404.HttpsTraffic"
        },
        "HttpsTraffic|1405": {
            $sum: "$1405.HttpsTraffic"
        },
        "HttpsTraffic|1406": {
            $sum: "$1406.HttpsTraffic"
        },
        "HttpsTraffic|1407": {
            $sum: "$1407.HttpsTraffic"
        },
        "HttpsTraffic|1408": {
            $sum: "$1408.HttpsTraffic"
        },
        "HttpsTraffic|1409": {
            $sum: "$1409.HttpsTraffic"
        },
        "HttpsTraffic|1410": {
            $sum: "$1410.HttpsTraffic"
        },
        "HttpsTraffic|1411": {
            $sum: "$1411.HttpsTraffic"
        },
        "HttpsTraffic|1412": {
            $sum: "$1412.HttpsTraffic"
        },
        "HttpsTraffic|1413": {
            $sum: "$1413.HttpsTraffic"
        },
        "HttpsTraffic|1414": {
            $sum: "$1414.HttpsTraffic"
        },
        "HttpsTraffic|1415": {
            $sum: "$1415.HttpsTraffic"
        },
        "HttpsTraffic|1416": {
            $sum: "$1416.HttpsTraffic"
        },
        "HttpsTraffic|1417": {
            $sum: "$1417.HttpsTraffic"
        },
        "HttpsTraffic|1418": {
            $sum: "$1418.HttpsTraffic"
        },
        "HttpsTraffic|1419": {
            $sum: "$1419.HttpsTraffic"
        },
        "HttpsTraffic|1420": {
            $sum: "$1420.HttpsTraffic"
        },
        "HttpsTraffic|1421": {
            $sum: "$1421.HttpsTraffic"
        },
        "HttpsTraffic|1422": {
            $sum: "$1422.HttpsTraffic"
        },
        "HttpsTraffic|1423": {
            $sum: "$1423.HttpsTraffic"
        },
        "HttpsTraffic|1424": {
            $sum: "$1424.HttpsTraffic"
        },
        "HttpsTraffic|1425": {
            $sum: "$1425.HttpsTraffic"
        },
        "HttpsTraffic|1426": {
            $sum: "$1426.HttpsTraffic"
        },
        "HttpsTraffic|1427": {
            $sum: "$1427.HttpsTraffic"
        },
        "HttpsTraffic|1428": {
            $sum: "$1428.HttpsTraffic"
        },
        "HttpsTraffic|1429": {
            $sum: "$1429.HttpsTraffic"
        },
        "HttpsTraffic|1430": {
            $sum: "$1430.HttpsTraffic"
        },
        "HttpsTraffic|1431": {
            $sum: "$1431.HttpsTraffic"
        },
        "HttpsTraffic|1432": {
            $sum: "$1432.HttpsTraffic"
        },
        "HttpsTraffic|1433": {
            $sum: "$1433.HttpsTraffic"
        },
        "HttpsTraffic|1434": {
            $sum: "$1434.HttpsTraffic"
        },
        "HttpsTraffic|1435": {
            $sum: "$1435.HttpsTraffic"
        },
        "HttpsTraffic|1436": {
            $sum: "$1436.HttpsTraffic"
        },
        "HttpsTraffic|1437": {
            $sum: "$1437.HttpsTraffic"
        },
        "HttpsTraffic|1438": {
            $sum: "$1438.HttpsTraffic"
        },
        "HttpsTraffic|1439": {
            $sum: "$1439.HttpsTraffic"
        },
        "HttpsTraffic|1440": {
            $sum: "$1440.HttpsTraffic"
        },
        "HttpsTraffic|1441": {
            $sum: "$1441.HttpsTraffic"
        },
        "HttpsTraffic|1442": {
            $sum: "$1442.HttpsTraffic"
        },
        "HttpsTraffic|1443": {
            $sum: "$1443.HttpsTraffic"
        },
        "HttpsTraffic|1444": {
            $sum: "$1444.HttpsTraffic"
        },
        "HttpsTraffic|1445": {
            $sum: "$1445.HttpsTraffic"
        },
        "HttpsTraffic|1446": {
            $sum: "$1446.HttpsTraffic"
        },
        "HttpsTraffic|1447": {
            $sum: "$1447.HttpsTraffic"
        },
        "HttpsTraffic|1448": {
            $sum: "$1448.HttpsTraffic"
        },
        "HttpsTraffic|1449": {
            $sum: "$1449.HttpsTraffic"
        },
        "HttpsTraffic|1450": {
            $sum: "$1450.HttpsTraffic"
        },
        "HttpsTraffic|1451": {
            $sum: "$1451.HttpsTraffic"
        },
        "HttpsTraffic|1452": {
            $sum: "$1452.HttpsTraffic"
        },
        "HttpsTraffic|1453": {
            $sum: "$1453.HttpsTraffic"
        },
        "HttpsTraffic|1454": {
            $sum: "$1454.HttpsTraffic"
        },
        "HttpsTraffic|1455": {
            $sum: "$1455.HttpsTraffic"
        },
        "HttpsTraffic|1456": {
            $sum: "$1456.HttpsTraffic"
        },
        "HttpsTraffic|1457": {
            $sum: "$1457.HttpsTraffic"
        },
        "HttpsTraffic|1458": {
            $sum: "$1458.HttpsTraffic"
        },
        "HttpsTraffic|1459": {
            $sum: "$1459.HttpsTraffic"
        },
        "HttpsTraffic|1500": {
            $sum: "$1500.HttpsTraffic"
        },
        "HttpsTraffic|1501": {
            $sum: "$1501.HttpsTraffic"
        },
        "HttpsTraffic|1502": {
            $sum: "$1502.HttpsTraffic"
        },
        "HttpsTraffic|1503": {
            $sum: "$1503.HttpsTraffic"
        },
        "HttpsTraffic|1504": {
            $sum: "$1504.HttpsTraffic"
        },
        "HttpsTraffic|1505": {
            $sum: "$1505.HttpsTraffic"
        },
        "HttpsTraffic|1506": {
            $sum: "$1506.HttpsTraffic"
        },
        "HttpsTraffic|1507": {
            $sum: "$1507.HttpsTraffic"
        },
        "HttpsTraffic|1508": {
            $sum: "$1508.HttpsTraffic"
        },
        "HttpsTraffic|1509": {
            $sum: "$1509.HttpsTraffic"
        },
        "HttpsTraffic|1510": {
            $sum: "$1510.HttpsTraffic"
        },
        "HttpsTraffic|1511": {
            $sum: "$1511.HttpsTraffic"
        },
        "HttpsTraffic|1512": {
            $sum: "$1512.HttpsTraffic"
        },
        "HttpsTraffic|1513": {
            $sum: "$1513.HttpsTraffic"
        },
        "HttpsTraffic|1514": {
            $sum: "$1514.HttpsTraffic"
        },
        "HttpsTraffic|1515": {
            $sum: "$1515.HttpsTraffic"
        },
        "HttpsTraffic|1516": {
            $sum: "$1516.HttpsTraffic"
        },
        "HttpsTraffic|1517": {
            $sum: "$1517.HttpsTraffic"
        },
        "HttpsTraffic|1518": {
            $sum: "$1518.HttpsTraffic"
        },
        "HttpsTraffic|1519": {
            $sum: "$1519.HttpsTraffic"
        },
        "HttpsTraffic|1520": {
            $sum: "$1520.HttpsTraffic"
        },
        "HttpsTraffic|1521": {
            $sum: "$1521.HttpsTraffic"
        },
        "HttpsTraffic|1522": {
            $sum: "$1522.HttpsTraffic"
        },
        "HttpsTraffic|1523": {
            $sum: "$1523.HttpsTraffic"
        },
        "HttpsTraffic|1524": {
            $sum: "$1524.HttpsTraffic"
        },
        "HttpsTraffic|1525": {
            $sum: "$1525.HttpsTraffic"
        },
        "HttpsTraffic|1526": {
            $sum: "$1526.HttpsTraffic"
        },
        "HttpsTraffic|1527": {
            $sum: "$1527.HttpsTraffic"
        },
        "HttpsTraffic|1528": {
            $sum: "$1528.HttpsTraffic"
        },
        "HttpsTraffic|1529": {
            $sum: "$1529.HttpsTraffic"
        },
        "HttpsTraffic|1530": {
            $sum: "$1530.HttpsTraffic"
        },
        "HttpsTraffic|1531": {
            $sum: "$1531.HttpsTraffic"
        },
        "HttpsTraffic|1532": {
            $sum: "$1532.HttpsTraffic"
        },
        "HttpsTraffic|1533": {
            $sum: "$1533.HttpsTraffic"
        },
        "HttpsTraffic|1534": {
            $sum: "$1534.HttpsTraffic"
        },
        "HttpsTraffic|1535": {
            $sum: "$1535.HttpsTraffic"
        },
        "HttpsTraffic|1536": {
            $sum: "$1536.HttpsTraffic"
        },
        "HttpsTraffic|1537": {
            $sum: "$1537.HttpsTraffic"
        },
        "HttpsTraffic|1538": {
            $sum: "$1538.HttpsTraffic"
        },
        "HttpsTraffic|1539": {
            $sum: "$1539.HttpsTraffic"
        },
        "HttpsTraffic|1540": {
            $sum: "$1540.HttpsTraffic"
        },
        "HttpsTraffic|1541": {
            $sum: "$1541.HttpsTraffic"
        },
        "HttpsTraffic|1542": {
            $sum: "$1542.HttpsTraffic"
        },
        "HttpsTraffic|1543": {
            $sum: "$1543.HttpsTraffic"
        },
        "HttpsTraffic|1544": {
            $sum: "$1544.HttpsTraffic"
        },
        "HttpsTraffic|1545": {
            $sum: "$1545.HttpsTraffic"
        },
        "HttpsTraffic|1546": {
            $sum: "$1546.HttpsTraffic"
        },
        "HttpsTraffic|1547": {
            $sum: "$1547.HttpsTraffic"
        },
        "HttpsTraffic|1548": {
            $sum: "$1548.HttpsTraffic"
        },
        "HttpsTraffic|1549": {
            $sum: "$1549.HttpsTraffic"
        },
        "HttpsTraffic|1550": {
            $sum: "$1550.HttpsTraffic"
        },
        "HttpsTraffic|1551": {
            $sum: "$1551.HttpsTraffic"
        },
        "HttpsTraffic|1552": {
            $sum: "$1552.HttpsTraffic"
        },
        "HttpsTraffic|1553": {
            $sum: "$1553.HttpsTraffic"
        },
        "HttpsTraffic|1554": {
            $sum: "$1554.HttpsTraffic"
        },
        "HttpsTraffic|1555": {
            $sum: "$1555.HttpsTraffic"
        },
        "HttpsTraffic|1556": {
            $sum: "$1556.HttpsTraffic"
        },
        "HttpsTraffic|1557": {
            $sum: "$1557.HttpsTraffic"
        },
        "HttpsTraffic|1558": {
            $sum: "$1558.HttpsTraffic"
        },
        "HttpsTraffic|1559": {
            $sum: "$1559.HttpsTraffic"
        },
        "HttpsTraffic|1600": {
            $sum: "$1600.HttpsTraffic"
        },
        "HttpsTraffic|1601": {
            $sum: "$1601.HttpsTraffic"
        },
        "HttpsTraffic|1602": {
            $sum: "$1602.HttpsTraffic"
        },
        "HttpsTraffic|1603": {
            $sum: "$1603.HttpsTraffic"
        },
        "HttpsTraffic|1604": {
            $sum: "$1604.HttpsTraffic"
        },
        "HttpsTraffic|1605": {
            $sum: "$1605.HttpsTraffic"
        },
        "HttpsTraffic|1606": {
            $sum: "$1606.HttpsTraffic"
        },
        "HttpsTraffic|1607": {
            $sum: "$1607.HttpsTraffic"
        },
        "HttpsTraffic|1608": {
            $sum: "$1608.HttpsTraffic"
        },
        "HttpsTraffic|1609": {
            $sum: "$1609.HttpsTraffic"
        },
        "HttpsTraffic|1610": {
            $sum: "$1610.HttpsTraffic"
        },
        "HttpsTraffic|1611": {
            $sum: "$1611.HttpsTraffic"
        },
        "HttpsTraffic|1612": {
            $sum: "$1612.HttpsTraffic"
        },
        "HttpsTraffic|1613": {
            $sum: "$1613.HttpsTraffic"
        },
        "HttpsTraffic|1614": {
            $sum: "$1614.HttpsTraffic"
        },
        "HttpsTraffic|1615": {
            $sum: "$1615.HttpsTraffic"
        },
        "HttpsTraffic|1616": {
            $sum: "$1616.HttpsTraffic"
        },
        "HttpsTraffic|1617": {
            $sum: "$1617.HttpsTraffic"
        },
        "HttpsTraffic|1618": {
            $sum: "$1618.HttpsTraffic"
        },
        "HttpsTraffic|1619": {
            $sum: "$1619.HttpsTraffic"
        },
        "HttpsTraffic|1620": {
            $sum: "$1620.HttpsTraffic"
        },
        "HttpsTraffic|1621": {
            $sum: "$1621.HttpsTraffic"
        },
        "HttpsTraffic|1622": {
            $sum: "$1622.HttpsTraffic"
        },
        "HttpsTraffic|1623": {
            $sum: "$1623.HttpsTraffic"
        },
        "HttpsTraffic|1624": {
            $sum: "$1624.HttpsTraffic"
        },
        "HttpsTraffic|1625": {
            $sum: "$1625.HttpsTraffic"
        },
        "HttpsTraffic|1626": {
            $sum: "$1626.HttpsTraffic"
        },
        "HttpsTraffic|1627": {
            $sum: "$1627.HttpsTraffic"
        },
        "HttpsTraffic|1628": {
            $sum: "$1628.HttpsTraffic"
        },
        "HttpsTraffic|1629": {
            $sum: "$1629.HttpsTraffic"
        },
        "HttpsTraffic|1630": {
            $sum: "$1630.HttpsTraffic"
        },
        "HttpsTraffic|1631": {
            $sum: "$1631.HttpsTraffic"
        },
        "HttpsTraffic|1632": {
            $sum: "$1632.HttpsTraffic"
        },
        "HttpsTraffic|1633": {
            $sum: "$1633.HttpsTraffic"
        },
        "HttpsTraffic|1634": {
            $sum: "$1634.HttpsTraffic"
        },
        "HttpsTraffic|1635": {
            $sum: "$1635.HttpsTraffic"
        },
        "HttpsTraffic|1636": {
            $sum: "$1636.HttpsTraffic"
        },
        "HttpsTraffic|1637": {
            $sum: "$1637.HttpsTraffic"
        },
        "HttpsTraffic|1638": {
            $sum: "$1638.HttpsTraffic"
        },
        "HttpsTraffic|1639": {
            $sum: "$1639.HttpsTraffic"
        },
        "HttpsTraffic|1640": {
            $sum: "$1640.HttpsTraffic"
        },
        "HttpsTraffic|1641": {
            $sum: "$1641.HttpsTraffic"
        },
        "HttpsTraffic|1642": {
            $sum: "$1642.HttpsTraffic"
        },
        "HttpsTraffic|1643": {
            $sum: "$1643.HttpsTraffic"
        },
        "HttpsTraffic|1644": {
            $sum: "$1644.HttpsTraffic"
        },
        "HttpsTraffic|1645": {
            $sum: "$1645.HttpsTraffic"
        },
        "HttpsTraffic|1646": {
            $sum: "$1646.HttpsTraffic"
        },
        "HttpsTraffic|1647": {
            $sum: "$1647.HttpsTraffic"
        },
        "HttpsTraffic|1648": {
            $sum: "$1648.HttpsTraffic"
        },
        "HttpsTraffic|1649": {
            $sum: "$1649.HttpsTraffic"
        },
        "HttpsTraffic|1650": {
            $sum: "$1650.HttpsTraffic"
        },
        "HttpsTraffic|1651": {
            $sum: "$1651.HttpsTraffic"
        },
        "HttpsTraffic|1652": {
            $sum: "$1652.HttpsTraffic"
        },
        "HttpsTraffic|1653": {
            $sum: "$1653.HttpsTraffic"
        },
        "HttpsTraffic|1654": {
            $sum: "$1654.HttpsTraffic"
        },
        "HttpsTraffic|1655": {
            $sum: "$1655.HttpsTraffic"
        },
        "HttpsTraffic|1656": {
            $sum: "$1656.HttpsTraffic"
        },
        "HttpsTraffic|1657": {
            $sum: "$1657.HttpsTraffic"
        },
        "HttpsTraffic|1658": {
            $sum: "$1658.HttpsTraffic"
        },
        "HttpsTraffic|1659": {
            $sum: "$1659.HttpsTraffic"
        },
        "HttpsTraffic|1700": {
            $sum: "$1700.HttpsTraffic"
        },
        "HttpsTraffic|1701": {
            $sum: "$1701.HttpsTraffic"
        },
        "HttpsTraffic|1702": {
            $sum: "$1702.HttpsTraffic"
        },
        "HttpsTraffic|1703": {
            $sum: "$1703.HttpsTraffic"
        },
        "HttpsTraffic|1704": {
            $sum: "$1704.HttpsTraffic"
        },
        "HttpsTraffic|1705": {
            $sum: "$1705.HttpsTraffic"
        },
        "HttpsTraffic|1706": {
            $sum: "$1706.HttpsTraffic"
        },
        "HttpsTraffic|1707": {
            $sum: "$1707.HttpsTraffic"
        },
        "HttpsTraffic|1708": {
            $sum: "$1708.HttpsTraffic"
        },
        "HttpsTraffic|1709": {
            $sum: "$1709.HttpsTraffic"
        },
        "HttpsTraffic|1710": {
            $sum: "$1710.HttpsTraffic"
        },
        "HttpsTraffic|1711": {
            $sum: "$1711.HttpsTraffic"
        },
        "HttpsTraffic|1712": {
            $sum: "$1712.HttpsTraffic"
        },
        "HttpsTraffic|1713": {
            $sum: "$1713.HttpsTraffic"
        },
        "HttpsTraffic|1714": {
            $sum: "$1714.HttpsTraffic"
        },
        "HttpsTraffic|1715": {
            $sum: "$1715.HttpsTraffic"
        },
        "HttpsTraffic|1716": {
            $sum: "$1716.HttpsTraffic"
        },
        "HttpsTraffic|1717": {
            $sum: "$1717.HttpsTraffic"
        },
        "HttpsTraffic|1718": {
            $sum: "$1718.HttpsTraffic"
        },
        "HttpsTraffic|1719": {
            $sum: "$1719.HttpsTraffic"
        },
        "HttpsTraffic|1720": {
            $sum: "$1720.HttpsTraffic"
        },
        "HttpsTraffic|1721": {
            $sum: "$1721.HttpsTraffic"
        },
        "HttpsTraffic|1722": {
            $sum: "$1722.HttpsTraffic"
        },
        "HttpsTraffic|1723": {
            $sum: "$1723.HttpsTraffic"
        },
        "HttpsTraffic|1724": {
            $sum: "$1724.HttpsTraffic"
        },
        "HttpsTraffic|1725": {
            $sum: "$1725.HttpsTraffic"
        },
        "HttpsTraffic|1726": {
            $sum: "$1726.HttpsTraffic"
        },
        "HttpsTraffic|1727": {
            $sum: "$1727.HttpsTraffic"
        },
        "HttpsTraffic|1728": {
            $sum: "$1728.HttpsTraffic"
        },
        "HttpsTraffic|1729": {
            $sum: "$1729.HttpsTraffic"
        },
        "HttpsTraffic|1730": {
            $sum: "$1730.HttpsTraffic"
        },
        "HttpsTraffic|1731": {
            $sum: "$1731.HttpsTraffic"
        },
        "HttpsTraffic|1732": {
            $sum: "$1732.HttpsTraffic"
        },
        "HttpsTraffic|1733": {
            $sum: "$1733.HttpsTraffic"
        },
        "HttpsTraffic|1734": {
            $sum: "$1734.HttpsTraffic"
        },
        "HttpsTraffic|1735": {
            $sum: "$1735.HttpsTraffic"
        },
        "HttpsTraffic|1736": {
            $sum: "$1736.HttpsTraffic"
        },
        "HttpsTraffic|1737": {
            $sum: "$1737.HttpsTraffic"
        },
        "HttpsTraffic|1738": {
            $sum: "$1738.HttpsTraffic"
        },
        "HttpsTraffic|1739": {
            $sum: "$1739.HttpsTraffic"
        },
        "HttpsTraffic|1740": {
            $sum: "$1740.HttpsTraffic"
        },
        "HttpsTraffic|1741": {
            $sum: "$1741.HttpsTraffic"
        },
        "HttpsTraffic|1742": {
            $sum: "$1742.HttpsTraffic"
        },
        "HttpsTraffic|1743": {
            $sum: "$1743.HttpsTraffic"
        },
        "HttpsTraffic|1744": {
            $sum: "$1744.HttpsTraffic"
        },
        "HttpsTraffic|1745": {
            $sum: "$1745.HttpsTraffic"
        },
        "HttpsTraffic|1746": {
            $sum: "$1746.HttpsTraffic"
        },
        "HttpsTraffic|1747": {
            $sum: "$1747.HttpsTraffic"
        },
        "HttpsTraffic|1748": {
            $sum: "$1748.HttpsTraffic"
        },
        "HttpsTraffic|1749": {
            $sum: "$1749.HttpsTraffic"
        },
        "HttpsTraffic|1750": {
            $sum: "$1750.HttpsTraffic"
        },
        "HttpsTraffic|1751": {
            $sum: "$1751.HttpsTraffic"
        },
        "HttpsTraffic|1752": {
            $sum: "$1752.HttpsTraffic"
        },
        "HttpsTraffic|1753": {
            $sum: "$1753.HttpsTraffic"
        },
        "HttpsTraffic|1754": {
            $sum: "$1754.HttpsTraffic"
        },
        "HttpsTraffic|1755": {
            $sum: "$1755.HttpsTraffic"
        },
        "HttpsTraffic|1756": {
            $sum: "$1756.HttpsTraffic"
        },
        "HttpsTraffic|1757": {
            $sum: "$1757.HttpsTraffic"
        },
        "HttpsTraffic|1758": {
            $sum: "$1758.HttpsTraffic"
        },
        "HttpsTraffic|1759": {
            $sum: "$1759.HttpsTraffic"
        },
        "HttpsTraffic|1800": {
            $sum: "$1800.HttpsTraffic"
        },
        "HttpsTraffic|1801": {
            $sum: "$1801.HttpsTraffic"
        },
        "HttpsTraffic|1802": {
            $sum: "$1802.HttpsTraffic"
        },
        "HttpsTraffic|1803": {
            $sum: "$1803.HttpsTraffic"
        },
        "HttpsTraffic|1804": {
            $sum: "$1804.HttpsTraffic"
        },
        "HttpsTraffic|1805": {
            $sum: "$1805.HttpsTraffic"
        },
        "HttpsTraffic|1806": {
            $sum: "$1806.HttpsTraffic"
        },
        "HttpsTraffic|1807": {
            $sum: "$1807.HttpsTraffic"
        },
        "HttpsTraffic|1808": {
            $sum: "$1808.HttpsTraffic"
        },
        "HttpsTraffic|1809": {
            $sum: "$1809.HttpsTraffic"
        },
        "HttpsTraffic|1810": {
            $sum: "$1810.HttpsTraffic"
        },
        "HttpsTraffic|1811": {
            $sum: "$1811.HttpsTraffic"
        },
        "HttpsTraffic|1812": {
            $sum: "$1812.HttpsTraffic"
        },
        "HttpsTraffic|1813": {
            $sum: "$1813.HttpsTraffic"
        },
        "HttpsTraffic|1814": {
            $sum: "$1814.HttpsTraffic"
        },
        "HttpsTraffic|1815": {
            $sum: "$1815.HttpsTraffic"
        },
        "HttpsTraffic|1816": {
            $sum: "$1816.HttpsTraffic"
        },
        "HttpsTraffic|1817": {
            $sum: "$1817.HttpsTraffic"
        },
        "HttpsTraffic|1818": {
            $sum: "$1818.HttpsTraffic"
        },
        "HttpsTraffic|1819": {
            $sum: "$1819.HttpsTraffic"
        },
        "HttpsTraffic|1820": {
            $sum: "$1820.HttpsTraffic"
        },
        "HttpsTraffic|1821": {
            $sum: "$1821.HttpsTraffic"
        },
        "HttpsTraffic|1822": {
            $sum: "$1822.HttpsTraffic"
        },
        "HttpsTraffic|1823": {
            $sum: "$1823.HttpsTraffic"
        },
        "HttpsTraffic|1824": {
            $sum: "$1824.HttpsTraffic"
        },
        "HttpsTraffic|1825": {
            $sum: "$1825.HttpsTraffic"
        },
        "HttpsTraffic|1826": {
            $sum: "$1826.HttpsTraffic"
        },
        "HttpsTraffic|1827": {
            $sum: "$1827.HttpsTraffic"
        },
        "HttpsTraffic|1828": {
            $sum: "$1828.HttpsTraffic"
        },
        "HttpsTraffic|1829": {
            $sum: "$1829.HttpsTraffic"
        },
        "HttpsTraffic|1830": {
            $sum: "$1830.HttpsTraffic"
        },
        "HttpsTraffic|1831": {
            $sum: "$1831.HttpsTraffic"
        },
        "HttpsTraffic|1832": {
            $sum: "$1832.HttpsTraffic"
        },
        "HttpsTraffic|1833": {
            $sum: "$1833.HttpsTraffic"
        },
        "HttpsTraffic|1834": {
            $sum: "$1834.HttpsTraffic"
        },
        "HttpsTraffic|1835": {
            $sum: "$1835.HttpsTraffic"
        },
        "HttpsTraffic|1836": {
            $sum: "$1836.HttpsTraffic"
        },
        "HttpsTraffic|1837": {
            $sum: "$1837.HttpsTraffic"
        },
        "HttpsTraffic|1838": {
            $sum: "$1838.HttpsTraffic"
        },
        "HttpsTraffic|1839": {
            $sum: "$1839.HttpsTraffic"
        },
        "HttpsTraffic|1840": {
            $sum: "$1840.HttpsTraffic"
        },
        "HttpsTraffic|1841": {
            $sum: "$1841.HttpsTraffic"
        },
        "HttpsTraffic|1842": {
            $sum: "$1842.HttpsTraffic"
        },
        "HttpsTraffic|1843": {
            $sum: "$1843.HttpsTraffic"
        },
        "HttpsTraffic|1844": {
            $sum: "$1844.HttpsTraffic"
        },
        "HttpsTraffic|1845": {
            $sum: "$1845.HttpsTraffic"
        },
        "HttpsTraffic|1846": {
            $sum: "$1846.HttpsTraffic"
        },
        "HttpsTraffic|1847": {
            $sum: "$1847.HttpsTraffic"
        },
        "HttpsTraffic|1848": {
            $sum: "$1848.HttpsTraffic"
        },
        "HttpsTraffic|1849": {
            $sum: "$1849.HttpsTraffic"
        },
        "HttpsTraffic|1850": {
            $sum: "$1850.HttpsTraffic"
        },
        "HttpsTraffic|1851": {
            $sum: "$1851.HttpsTraffic"
        },
        "HttpsTraffic|1852": {
            $sum: "$1852.HttpsTraffic"
        },
        "HttpsTraffic|1853": {
            $sum: "$1853.HttpsTraffic"
        },
        "HttpsTraffic|1854": {
            $sum: "$1854.HttpsTraffic"
        },
        "HttpsTraffic|1855": {
            $sum: "$1855.HttpsTraffic"
        },
        "HttpsTraffic|1856": {
            $sum: "$1856.HttpsTraffic"
        },
        "HttpsTraffic|1857": {
            $sum: "$1857.HttpsTraffic"
        },
        "HttpsTraffic|1858": {
            $sum: "$1858.HttpsTraffic"
        },
        "HttpsTraffic|1859": {
            $sum: "$1859.HttpsTraffic"
        },
        "HttpsTraffic|1900": {
            $sum: "$1900.HttpsTraffic"
        },
        "HttpsTraffic|1901": {
            $sum: "$1901.HttpsTraffic"
        },
        "HttpsTraffic|1902": {
            $sum: "$1902.HttpsTraffic"
        },
        "HttpsTraffic|1903": {
            $sum: "$1903.HttpsTraffic"
        },
        "HttpsTraffic|1904": {
            $sum: "$1904.HttpsTraffic"
        },
        "HttpsTraffic|1905": {
            $sum: "$1905.HttpsTraffic"
        },
        "HttpsTraffic|1906": {
            $sum: "$1906.HttpsTraffic"
        },
        "HttpsTraffic|1907": {
            $sum: "$1907.HttpsTraffic"
        },
        "HttpsTraffic|1908": {
            $sum: "$1908.HttpsTraffic"
        },
        "HttpsTraffic|1909": {
            $sum: "$1909.HttpsTraffic"
        },
        "HttpsTraffic|1910": {
            $sum: "$1910.HttpsTraffic"
        },
        "HttpsTraffic|1911": {
            $sum: "$1911.HttpsTraffic"
        },
        "HttpsTraffic|1912": {
            $sum: "$1912.HttpsTraffic"
        },
        "HttpsTraffic|1913": {
            $sum: "$1913.HttpsTraffic"
        },
        "HttpsTraffic|1914": {
            $sum: "$1914.HttpsTraffic"
        },
        "HttpsTraffic|1915": {
            $sum: "$1915.HttpsTraffic"
        },
        "HttpsTraffic|1916": {
            $sum: "$1916.HttpsTraffic"
        },
        "HttpsTraffic|1917": {
            $sum: "$1917.HttpsTraffic"
        },
        "HttpsTraffic|1918": {
            $sum: "$1918.HttpsTraffic"
        },
        "HttpsTraffic|1919": {
            $sum: "$1919.HttpsTraffic"
        },
        "HttpsTraffic|1920": {
            $sum: "$1920.HttpsTraffic"
        },
        "HttpsTraffic|1921": {
            $sum: "$1921.HttpsTraffic"
        },
        "HttpsTraffic|1922": {
            $sum: "$1922.HttpsTraffic"
        },
        "HttpsTraffic|1923": {
            $sum: "$1923.HttpsTraffic"
        },
        "HttpsTraffic|1924": {
            $sum: "$1924.HttpsTraffic"
        },
        "HttpsTraffic|1925": {
            $sum: "$1925.HttpsTraffic"
        },
        "HttpsTraffic|1926": {
            $sum: "$1926.HttpsTraffic"
        },
        "HttpsTraffic|1927": {
            $sum: "$1927.HttpsTraffic"
        },
        "HttpsTraffic|1928": {
            $sum: "$1928.HttpsTraffic"
        },
        "HttpsTraffic|1929": {
            $sum: "$1929.HttpsTraffic"
        },
        "HttpsTraffic|1930": {
            $sum: "$1930.HttpsTraffic"
        },
        "HttpsTraffic|1931": {
            $sum: "$1931.HttpsTraffic"
        },
        "HttpsTraffic|1932": {
            $sum: "$1932.HttpsTraffic"
        },
        "HttpsTraffic|1933": {
            $sum: "$1933.HttpsTraffic"
        },
        "HttpsTraffic|1934": {
            $sum: "$1934.HttpsTraffic"
        },
        "HttpsTraffic|1935": {
            $sum: "$1935.HttpsTraffic"
        },
        "HttpsTraffic|1936": {
            $sum: "$1936.HttpsTraffic"
        },
        "HttpsTraffic|1937": {
            $sum: "$1937.HttpsTraffic"
        },
        "HttpsTraffic|1938": {
            $sum: "$1938.HttpsTraffic"
        },
        "HttpsTraffic|1939": {
            $sum: "$1939.HttpsTraffic"
        },
        "HttpsTraffic|1940": {
            $sum: "$1940.HttpsTraffic"
        },
        "HttpsTraffic|1941": {
            $sum: "$1941.HttpsTraffic"
        },
        "HttpsTraffic|1942": {
            $sum: "$1942.HttpsTraffic"
        },
        "HttpsTraffic|1943": {
            $sum: "$1943.HttpsTraffic"
        },
        "HttpsTraffic|1944": {
            $sum: "$1944.HttpsTraffic"
        },
        "HttpsTraffic|1945": {
            $sum: "$1945.HttpsTraffic"
        },
        "HttpsTraffic|1946": {
            $sum: "$1946.HttpsTraffic"
        },
        "HttpsTraffic|1947": {
            $sum: "$1947.HttpsTraffic"
        },
        "HttpsTraffic|1948": {
            $sum: "$1948.HttpsTraffic"
        },
        "HttpsTraffic|1949": {
            $sum: "$1949.HttpsTraffic"
        },
        "HttpsTraffic|1950": {
            $sum: "$1950.HttpsTraffic"
        },
        "HttpsTraffic|1951": {
            $sum: "$1951.HttpsTraffic"
        },
        "HttpsTraffic|1952": {
            $sum: "$1952.HttpsTraffic"
        },
        "HttpsTraffic|1953": {
            $sum: "$1953.HttpsTraffic"
        },
        "HttpsTraffic|1954": {
            $sum: "$1954.HttpsTraffic"
        },
        "HttpsTraffic|1955": {
            $sum: "$1955.HttpsTraffic"
        },
        "HttpsTraffic|1956": {
            $sum: "$1956.HttpsTraffic"
        },
        "HttpsTraffic|1957": {
            $sum: "$1957.HttpsTraffic"
        },
        "HttpsTraffic|1958": {
            $sum: "$1958.HttpsTraffic"
        },
        "HttpsTraffic|1959": {
            $sum: "$1959.HttpsTraffic"
        },
        "HttpsTraffic|2000": {
            $sum: "$2000.HttpsTraffic"
        },
        "HttpsTraffic|2001": {
            $sum: "$2001.HttpsTraffic"
        },
        "HttpsTraffic|2002": {
            $sum: "$2002.HttpsTraffic"
        },
        "HttpsTraffic|2003": {
            $sum: "$2003.HttpsTraffic"
        },
        "HttpsTraffic|2004": {
            $sum: "$2004.HttpsTraffic"
        },
        "HttpsTraffic|2005": {
            $sum: "$2005.HttpsTraffic"
        },
        "HttpsTraffic|2006": {
            $sum: "$2006.HttpsTraffic"
        },
        "HttpsTraffic|2007": {
            $sum: "$2007.HttpsTraffic"
        },
        "HttpsTraffic|2008": {
            $sum: "$2008.HttpsTraffic"
        },
        "HttpsTraffic|2009": {
            $sum: "$2009.HttpsTraffic"
        },
        "HttpsTraffic|2010": {
            $sum: "$2010.HttpsTraffic"
        },
        "HttpsTraffic|2011": {
            $sum: "$2011.HttpsTraffic"
        },
        "HttpsTraffic|2012": {
            $sum: "$2012.HttpsTraffic"
        },
        "HttpsTraffic|2013": {
            $sum: "$2013.HttpsTraffic"
        },
        "HttpsTraffic|2014": {
            $sum: "$2014.HttpsTraffic"
        },
        "HttpsTraffic|2015": {
            $sum: "$2015.HttpsTraffic"
        },
        "HttpsTraffic|2016": {
            $sum: "$2016.HttpsTraffic"
        },
        "HttpsTraffic|2017": {
            $sum: "$2017.HttpsTraffic"
        },
        "HttpsTraffic|2018": {
            $sum: "$2018.HttpsTraffic"
        },
        "HttpsTraffic|2019": {
            $sum: "$2019.HttpsTraffic"
        },
        "HttpsTraffic|2020": {
            $sum: "$2020.HttpsTraffic"
        },
        "HttpsTraffic|2021": {
            $sum: "$2021.HttpsTraffic"
        },
        "HttpsTraffic|2022": {
            $sum: "$2022.HttpsTraffic"
        },
        "HttpsTraffic|2023": {
            $sum: "$2023.HttpsTraffic"
        },
        "HttpsTraffic|2024": {
            $sum: "$2024.HttpsTraffic"
        },
        "HttpsTraffic|2025": {
            $sum: "$2025.HttpsTraffic"
        },
        "HttpsTraffic|2026": {
            $sum: "$2026.HttpsTraffic"
        },
        "HttpsTraffic|2027": {
            $sum: "$2027.HttpsTraffic"
        },
        "HttpsTraffic|2028": {
            $sum: "$2028.HttpsTraffic"
        },
        "HttpsTraffic|2029": {
            $sum: "$2029.HttpsTraffic"
        },
        "HttpsTraffic|2030": {
            $sum: "$2030.HttpsTraffic"
        },
        "HttpsTraffic|2031": {
            $sum: "$2031.HttpsTraffic"
        },
        "HttpsTraffic|2032": {
            $sum: "$2032.HttpsTraffic"
        },
        "HttpsTraffic|2033": {
            $sum: "$2033.HttpsTraffic"
        },
        "HttpsTraffic|2034": {
            $sum: "$2034.HttpsTraffic"
        },
        "HttpsTraffic|2035": {
            $sum: "$2035.HttpsTraffic"
        },
        "HttpsTraffic|2036": {
            $sum: "$2036.HttpsTraffic"
        },
        "HttpsTraffic|2037": {
            $sum: "$2037.HttpsTraffic"
        },
        "HttpsTraffic|2038": {
            $sum: "$2038.HttpsTraffic"
        },
        "HttpsTraffic|2039": {
            $sum: "$2039.HttpsTraffic"
        },
        "HttpsTraffic|2040": {
            $sum: "$2040.HttpsTraffic"
        },
        "HttpsTraffic|2041": {
            $sum: "$2041.HttpsTraffic"
        },
        "HttpsTraffic|2042": {
            $sum: "$2042.HttpsTraffic"
        },
        "HttpsTraffic|2043": {
            $sum: "$2043.HttpsTraffic"
        },
        "HttpsTraffic|2044": {
            $sum: "$2044.HttpsTraffic"
        },
        "HttpsTraffic|2045": {
            $sum: "$2045.HttpsTraffic"
        },
        "HttpsTraffic|2046": {
            $sum: "$2046.HttpsTraffic"
        },
        "HttpsTraffic|2047": {
            $sum: "$2047.HttpsTraffic"
        },
        "HttpsTraffic|2048": {
            $sum: "$2048.HttpsTraffic"
        },
        "HttpsTraffic|2049": {
            $sum: "$2049.HttpsTraffic"
        },
        "HttpsTraffic|2050": {
            $sum: "$2050.HttpsTraffic"
        },
        "HttpsTraffic|2051": {
            $sum: "$2051.HttpsTraffic"
        },
        "HttpsTraffic|2052": {
            $sum: "$2052.HttpsTraffic"
        },
        "HttpsTraffic|2053": {
            $sum: "$2053.HttpsTraffic"
        },
        "HttpsTraffic|2054": {
            $sum: "$2054.HttpsTraffic"
        },
        "HttpsTraffic|2055": {
            $sum: "$2055.HttpsTraffic"
        },
        "HttpsTraffic|2056": {
            $sum: "$2056.HttpsTraffic"
        },
        "HttpsTraffic|2057": {
            $sum: "$2057.HttpsTraffic"
        },
        "HttpsTraffic|2058": {
            $sum: "$2058.HttpsTraffic"
        },
        "HttpsTraffic|2059": {
            $sum: "$2059.HttpsTraffic"
        },
        "HttpsTraffic|2100": {
            $sum: "$2100.HttpsTraffic"
        },
        "HttpsTraffic|2101": {
            $sum: "$2101.HttpsTraffic"
        },
        "HttpsTraffic|2102": {
            $sum: "$2102.HttpsTraffic"
        },
        "HttpsTraffic|2103": {
            $sum: "$2103.HttpsTraffic"
        },
        "HttpsTraffic|2104": {
            $sum: "$2104.HttpsTraffic"
        },
        "HttpsTraffic|2105": {
            $sum: "$2105.HttpsTraffic"
        },
        "HttpsTraffic|2106": {
            $sum: "$2106.HttpsTraffic"
        },
        "HttpsTraffic|2107": {
            $sum: "$2107.HttpsTraffic"
        },
        "HttpsTraffic|2108": {
            $sum: "$2108.HttpsTraffic"
        },
        "HttpsTraffic|2109": {
            $sum: "$2109.HttpsTraffic"
        },
        "HttpsTraffic|2110": {
            $sum: "$2110.HttpsTraffic"
        },
        "HttpsTraffic|2111": {
            $sum: "$2111.HttpsTraffic"
        },
        "HttpsTraffic|2112": {
            $sum: "$2112.HttpsTraffic"
        },
        "HttpsTraffic|2113": {
            $sum: "$2113.HttpsTraffic"
        },
        "HttpsTraffic|2114": {
            $sum: "$2114.HttpsTraffic"
        },
        "HttpsTraffic|2115": {
            $sum: "$2115.HttpsTraffic"
        },
        "HttpsTraffic|2116": {
            $sum: "$2116.HttpsTraffic"
        },
        "HttpsTraffic|2117": {
            $sum: "$2117.HttpsTraffic"
        },
        "HttpsTraffic|2118": {
            $sum: "$2118.HttpsTraffic"
        },
        "HttpsTraffic|2119": {
            $sum: "$2119.HttpsTraffic"
        },
        "HttpsTraffic|2120": {
            $sum: "$2120.HttpsTraffic"
        },
        "HttpsTraffic|2121": {
            $sum: "$2121.HttpsTraffic"
        },
        "HttpsTraffic|2122": {
            $sum: "$2122.HttpsTraffic"
        },
        "HttpsTraffic|2123": {
            $sum: "$2123.HttpsTraffic"
        },
        "HttpsTraffic|2124": {
            $sum: "$2124.HttpsTraffic"
        },
        "HttpsTraffic|2125": {
            $sum: "$2125.HttpsTraffic"
        },
        "HttpsTraffic|2126": {
            $sum: "$2126.HttpsTraffic"
        },
        "HttpsTraffic|2127": {
            $sum: "$2127.HttpsTraffic"
        },
        "HttpsTraffic|2128": {
            $sum: "$2128.HttpsTraffic"
        },
        "HttpsTraffic|2129": {
            $sum: "$2129.HttpsTraffic"
        },
        "HttpsTraffic|2130": {
            $sum: "$2130.HttpsTraffic"
        },
        "HttpsTraffic|2131": {
            $sum: "$2131.HttpsTraffic"
        },
        "HttpsTraffic|2132": {
            $sum: "$2132.HttpsTraffic"
        },
        "HttpsTraffic|2133": {
            $sum: "$2133.HttpsTraffic"
        },
        "HttpsTraffic|2134": {
            $sum: "$2134.HttpsTraffic"
        },
        "HttpsTraffic|2135": {
            $sum: "$2135.HttpsTraffic"
        },
        "HttpsTraffic|2136": {
            $sum: "$2136.HttpsTraffic"
        },
        "HttpsTraffic|2137": {
            $sum: "$2137.HttpsTraffic"
        },
        "HttpsTraffic|2138": {
            $sum: "$2138.HttpsTraffic"
        },
        "HttpsTraffic|2139": {
            $sum: "$2139.HttpsTraffic"
        },
        "HttpsTraffic|2140": {
            $sum: "$2140.HttpsTraffic"
        },
        "HttpsTraffic|2141": {
            $sum: "$2141.HttpsTraffic"
        },
        "HttpsTraffic|2142": {
            $sum: "$2142.HttpsTraffic"
        },
        "HttpsTraffic|2143": {
            $sum: "$2143.HttpsTraffic"
        },
        "HttpsTraffic|2144": {
            $sum: "$2144.HttpsTraffic"
        },
        "HttpsTraffic|2145": {
            $sum: "$2145.HttpsTraffic"
        },
        "HttpsTraffic|2146": {
            $sum: "$2146.HttpsTraffic"
        },
        "HttpsTraffic|2147": {
            $sum: "$2147.HttpsTraffic"
        },
        "HttpsTraffic|2148": {
            $sum: "$2148.HttpsTraffic"
        },
        "HttpsTraffic|2149": {
            $sum: "$2149.HttpsTraffic"
        },
        "HttpsTraffic|2150": {
            $sum: "$2150.HttpsTraffic"
        },
        "HttpsTraffic|2151": {
            $sum: "$2151.HttpsTraffic"
        },
        "HttpsTraffic|2152": {
            $sum: "$2152.HttpsTraffic"
        },
        "HttpsTraffic|2153": {
            $sum: "$2153.HttpsTraffic"
        },
        "HttpsTraffic|2154": {
            $sum: "$2154.HttpsTraffic"
        },
        "HttpsTraffic|2155": {
            $sum: "$2155.HttpsTraffic"
        },
        "HttpsTraffic|2156": {
            $sum: "$2156.HttpsTraffic"
        },
        "HttpsTraffic|2157": {
            $sum: "$2157.HttpsTraffic"
        },
        "HttpsTraffic|2158": {
            $sum: "$2158.HttpsTraffic"
        },
        "HttpsTraffic|2159": {
            $sum: "$2159.HttpsTraffic"
        },
        "HttpsTraffic|2200": {
            $sum: "$2200.HttpsTraffic"
        },
        "HttpsTraffic|2201": {
            $sum: "$2201.HttpsTraffic"
        },
        "HttpsTraffic|2202": {
            $sum: "$2202.HttpsTraffic"
        },
        "HttpsTraffic|2203": {
            $sum: "$2203.HttpsTraffic"
        },
        "HttpsTraffic|2204": {
            $sum: "$2204.HttpsTraffic"
        },
        "HttpsTraffic|2205": {
            $sum: "$2205.HttpsTraffic"
        },
        "HttpsTraffic|2206": {
            $sum: "$2206.HttpsTraffic"
        },
        "HttpsTraffic|2207": {
            $sum: "$2207.HttpsTraffic"
        },
        "HttpsTraffic|2208": {
            $sum: "$2208.HttpsTraffic"
        },
        "HttpsTraffic|2209": {
            $sum: "$2209.HttpsTraffic"
        },
        "HttpsTraffic|2210": {
            $sum: "$2210.HttpsTraffic"
        },
        "HttpsTraffic|2211": {
            $sum: "$2211.HttpsTraffic"
        },
        "HttpsTraffic|2212": {
            $sum: "$2212.HttpsTraffic"
        },
        "HttpsTraffic|2213": {
            $sum: "$2213.HttpsTraffic"
        },
        "HttpsTraffic|2214": {
            $sum: "$2214.HttpsTraffic"
        },
        "HttpsTraffic|2215": {
            $sum: "$2215.HttpsTraffic"
        },
        "HttpsTraffic|2216": {
            $sum: "$2216.HttpsTraffic"
        },
        "HttpsTraffic|2217": {
            $sum: "$2217.HttpsTraffic"
        },
        "HttpsTraffic|2218": {
            $sum: "$2218.HttpsTraffic"
        },
        "HttpsTraffic|2219": {
            $sum: "$2219.HttpsTraffic"
        },
        "HttpsTraffic|2220": {
            $sum: "$2220.HttpsTraffic"
        },
        "HttpsTraffic|2221": {
            $sum: "$2221.HttpsTraffic"
        },
        "HttpsTraffic|2222": {
            $sum: "$2222.HttpsTraffic"
        },
        "HttpsTraffic|2223": {
            $sum: "$2223.HttpsTraffic"
        },
        "HttpsTraffic|2224": {
            $sum: "$2224.HttpsTraffic"
        },
        "HttpsTraffic|2225": {
            $sum: "$2225.HttpsTraffic"
        },
        "HttpsTraffic|2226": {
            $sum: "$2226.HttpsTraffic"
        },
        "HttpsTraffic|2227": {
            $sum: "$2227.HttpsTraffic"
        },
        "HttpsTraffic|2228": {
            $sum: "$2228.HttpsTraffic"
        },
        "HttpsTraffic|2229": {
            $sum: "$2229.HttpsTraffic"
        },
        "HttpsTraffic|2230": {
            $sum: "$2230.HttpsTraffic"
        },
        "HttpsTraffic|2231": {
            $sum: "$2231.HttpsTraffic"
        },
        "HttpsTraffic|2232": {
            $sum: "$2232.HttpsTraffic"
        },
        "HttpsTraffic|2233": {
            $sum: "$2233.HttpsTraffic"
        },
        "HttpsTraffic|2234": {
            $sum: "$2234.HttpsTraffic"
        },
        "HttpsTraffic|2235": {
            $sum: "$2235.HttpsTraffic"
        },
        "HttpsTraffic|2236": {
            $sum: "$2236.HttpsTraffic"
        },
        "HttpsTraffic|2237": {
            $sum: "$2237.HttpsTraffic"
        },
        "HttpsTraffic|2238": {
            $sum: "$2238.HttpsTraffic"
        },
        "HttpsTraffic|2239": {
            $sum: "$2239.HttpsTraffic"
        },
        "HttpsTraffic|2240": {
            $sum: "$2240.HttpsTraffic"
        },
        "HttpsTraffic|2241": {
            $sum: "$2241.HttpsTraffic"
        },
        "HttpsTraffic|2242": {
            $sum: "$2242.HttpsTraffic"
        },
        "HttpsTraffic|2243": {
            $sum: "$2243.HttpsTraffic"
        },
        "HttpsTraffic|2244": {
            $sum: "$2244.HttpsTraffic"
        },
        "HttpsTraffic|2245": {
            $sum: "$2245.HttpsTraffic"
        },
        "HttpsTraffic|2246": {
            $sum: "$2246.HttpsTraffic"
        },
        "HttpsTraffic|2247": {
            $sum: "$2247.HttpsTraffic"
        },
        "HttpsTraffic|2248": {
            $sum: "$2248.HttpsTraffic"
        },
        "HttpsTraffic|2249": {
            $sum: "$2249.HttpsTraffic"
        },
        "HttpsTraffic|2250": {
            $sum: "$2250.HttpsTraffic"
        },
        "HttpsTraffic|2251": {
            $sum: "$2251.HttpsTraffic"
        },
        "HttpsTraffic|2252": {
            $sum: "$2252.HttpsTraffic"
        },
        "HttpsTraffic|2253": {
            $sum: "$2253.HttpsTraffic"
        },
        "HttpsTraffic|2254": {
            $sum: "$2254.HttpsTraffic"
        },
        "HttpsTraffic|2255": {
            $sum: "$2255.HttpsTraffic"
        },
        "HttpsTraffic|2256": {
            $sum: "$2256.HttpsTraffic"
        },
        "HttpsTraffic|2257": {
            $sum: "$2257.HttpsTraffic"
        },
        "HttpsTraffic|2258": {
            $sum: "$2258.HttpsTraffic"
        },
        "HttpsTraffic|2259": {
            $sum: "$2259.HttpsTraffic"
        },
        "HttpsTraffic|2300": {
            $sum: "$2300.HttpsTraffic"
        },
        "HttpsTraffic|2301": {
            $sum: "$2301.HttpsTraffic"
        },
        "HttpsTraffic|2302": {
            $sum: "$2302.HttpsTraffic"
        },
        "HttpsTraffic|2303": {
            $sum: "$2303.HttpsTraffic"
        },
        "HttpsTraffic|2304": {
            $sum: "$2304.HttpsTraffic"
        },
        "HttpsTraffic|2305": {
            $sum: "$2305.HttpsTraffic"
        },
        "HttpsTraffic|2306": {
            $sum: "$2306.HttpsTraffic"
        },
        "HttpsTraffic|2307": {
            $sum: "$2307.HttpsTraffic"
        },
        "HttpsTraffic|2308": {
            $sum: "$2308.HttpsTraffic"
        },
        "HttpsTraffic|2309": {
            $sum: "$2309.HttpsTraffic"
        },
        "HttpsTraffic|2310": {
            $sum: "$2310.HttpsTraffic"
        },
        "HttpsTraffic|2311": {
            $sum: "$2311.HttpsTraffic"
        },
        "HttpsTraffic|2312": {
            $sum: "$2312.HttpsTraffic"
        },
        "HttpsTraffic|2313": {
            $sum: "$2313.HttpsTraffic"
        },
        "HttpsTraffic|2314": {
            $sum: "$2314.HttpsTraffic"
        },
        "HttpsTraffic|2315": {
            $sum: "$2315.HttpsTraffic"
        },
        "HttpsTraffic|2316": {
            $sum: "$2316.HttpsTraffic"
        },
        "HttpsTraffic|2317": {
            $sum: "$2317.HttpsTraffic"
        },
        "HttpsTraffic|2318": {
            $sum: "$2318.HttpsTraffic"
        },
        "HttpsTraffic|2319": {
            $sum: "$2319.HttpsTraffic"
        },
        "HttpsTraffic|2320": {
            $sum: "$2320.HttpsTraffic"
        },
        "HttpsTraffic|2321": {
            $sum: "$2321.HttpsTraffic"
        },
        "HttpsTraffic|2322": {
            $sum: "$2322.HttpsTraffic"
        },
        "HttpsTraffic|2323": {
            $sum: "$2323.HttpsTraffic"
        },
        "HttpsTraffic|2324": {
            $sum: "$2324.HttpsTraffic"
        },
        "HttpsTraffic|2325": {
            $sum: "$2325.HttpsTraffic"
        },
        "HttpsTraffic|2326": {
            $sum: "$2326.HttpsTraffic"
        },
        "HttpsTraffic|2327": {
            $sum: "$2327.HttpsTraffic"
        },
        "HttpsTraffic|2328": {
            $sum: "$2328.HttpsTraffic"
        },
        "HttpsTraffic|2329": {
            $sum: "$2329.HttpsTraffic"
        },
        "HttpsTraffic|2330": {
            $sum: "$2330.HttpsTraffic"
        },
        "HttpsTraffic|2331": {
            $sum: "$2331.HttpsTraffic"
        },
        "HttpsTraffic|2332": {
            $sum: "$2332.HttpsTraffic"
        },
        "HttpsTraffic|2333": {
            $sum: "$2333.HttpsTraffic"
        },
        "HttpsTraffic|2334": {
            $sum: "$2334.HttpsTraffic"
        },
        "HttpsTraffic|2335": {
            $sum: "$2335.HttpsTraffic"
        },
        "HttpsTraffic|2336": {
            $sum: "$2336.HttpsTraffic"
        },
        "HttpsTraffic|2337": {
            $sum: "$2337.HttpsTraffic"
        },
        "HttpsTraffic|2338": {
            $sum: "$2338.HttpsTraffic"
        },
        "HttpsTraffic|2339": {
            $sum: "$2339.HttpsTraffic"
        },
        "HttpsTraffic|2340": {
            $sum: "$2340.HttpsTraffic"
        },
        "HttpsTraffic|2341": {
            $sum: "$2341.HttpsTraffic"
        },
        "HttpsTraffic|2342": {
            $sum: "$2342.HttpsTraffic"
        },
        "HttpsTraffic|2343": {
            $sum: "$2343.HttpsTraffic"
        },
        "HttpsTraffic|2344": {
            $sum: "$2344.HttpsTraffic"
        },
        "HttpsTraffic|2345": {
            $sum: "$2345.HttpsTraffic"
        },
        "HttpsTraffic|2346": {
            $sum: "$2346.HttpsTraffic"
        },
        "HttpsTraffic|2347": {
            $sum: "$2347.HttpsTraffic"
        },
        "HttpsTraffic|2348": {
            $sum: "$2348.HttpsTraffic"
        },
        "HttpsTraffic|2349": {
            $sum: "$2349.HttpsTraffic"
        },
        "HttpsTraffic|2350": {
            $sum: "$2350.HttpsTraffic"
        },
        "HttpsTraffic|2351": {
            $sum: "$2351.HttpsTraffic"
        },
        "HttpsTraffic|2352": {
            $sum: "$2352.HttpsTraffic"
        },
        "HttpsTraffic|2353": {
            $sum: "$2353.HttpsTraffic"
        },
        "HttpsTraffic|2354": {
            $sum: "$2354.HttpsTraffic"
        },
        "HttpsTraffic|2355": {
            $sum: "$2355.HttpsTraffic"
        },
        "HttpsTraffic|2356": {
            $sum: "$2356.HttpsTraffic"
        },
        "HttpsTraffic|2357": {
            $sum: "$2357.HttpsTraffic"
        },
        "HttpsTraffic|2358": {
            $sum: "$2358.HttpsTraffic"
        },
        "HttpsTraffic|2359": {
            $sum: "$2359.HttpsTraffic"
        },
        "IPV6Traffic|0000": {
            $sum: "$0000.IPV6Traffic"
        },
        "IPV6Traffic|0001": {
            $sum: "$0001.IPV6Traffic"
        },
        "IPV6Traffic|0002": {
            $sum: "$0002.IPV6Traffic"
        },
        "IPV6Traffic|0003": {
            $sum: "$0003.IPV6Traffic"
        },
        "IPV6Traffic|0004": {
            $sum: "$0004.IPV6Traffic"
        },
        "IPV6Traffic|0005": {
            $sum: "$0005.IPV6Traffic"
        },
        "IPV6Traffic|0006": {
            $sum: "$0006.IPV6Traffic"
        },
        "IPV6Traffic|0007": {
            $sum: "$0007.IPV6Traffic"
        },
        "IPV6Traffic|0008": {
            $sum: "$0008.IPV6Traffic"
        },
        "IPV6Traffic|0009": {
            $sum: "$0009.IPV6Traffic"
        },
        "IPV6Traffic|0010": {
            $sum: "$0010.IPV6Traffic"
        },
        "IPV6Traffic|0011": {
            $sum: "$0011.IPV6Traffic"
        },
        "IPV6Traffic|0012": {
            $sum: "$0012.IPV6Traffic"
        },
        "IPV6Traffic|0013": {
            $sum: "$0013.IPV6Traffic"
        },
        "IPV6Traffic|0014": {
            $sum: "$0014.IPV6Traffic"
        },
        "IPV6Traffic|0015": {
            $sum: "$0015.IPV6Traffic"
        },
        "IPV6Traffic|0016": {
            $sum: "$0016.IPV6Traffic"
        },
        "IPV6Traffic|0017": {
            $sum: "$0017.IPV6Traffic"
        },
        "IPV6Traffic|0018": {
            $sum: "$0018.IPV6Traffic"
        },
        "IPV6Traffic|0019": {
            $sum: "$0019.IPV6Traffic"
        },
        "IPV6Traffic|0020": {
            $sum: "$0020.IPV6Traffic"
        },
        "IPV6Traffic|0021": {
            $sum: "$0021.IPV6Traffic"
        },
        "IPV6Traffic|0022": {
            $sum: "$0022.IPV6Traffic"
        },
        "IPV6Traffic|0023": {
            $sum: "$0023.IPV6Traffic"
        },
        "IPV6Traffic|0024": {
            $sum: "$0024.IPV6Traffic"
        },
        "IPV6Traffic|0025": {
            $sum: "$0025.IPV6Traffic"
        },
        "IPV6Traffic|0026": {
            $sum: "$0026.IPV6Traffic"
        },
        "IPV6Traffic|0027": {
            $sum: "$0027.IPV6Traffic"
        },
        "IPV6Traffic|0028": {
            $sum: "$0028.IPV6Traffic"
        },
        "IPV6Traffic|0029": {
            $sum: "$0029.IPV6Traffic"
        },
        "IPV6Traffic|0030": {
            $sum: "$0030.IPV6Traffic"
        },
        "IPV6Traffic|0031": {
            $sum: "$0031.IPV6Traffic"
        },
        "IPV6Traffic|0032": {
            $sum: "$0032.IPV6Traffic"
        },
        "IPV6Traffic|0033": {
            $sum: "$0033.IPV6Traffic"
        },
        "IPV6Traffic|0034": {
            $sum: "$0034.IPV6Traffic"
        },
        "IPV6Traffic|0035": {
            $sum: "$0035.IPV6Traffic"
        },
        "IPV6Traffic|0036": {
            $sum: "$0036.IPV6Traffic"
        },
        "IPV6Traffic|0037": {
            $sum: "$0037.IPV6Traffic"
        },
        "IPV6Traffic|0038": {
            $sum: "$0038.IPV6Traffic"
        },
        "IPV6Traffic|0039": {
            $sum: "$0039.IPV6Traffic"
        },
        "IPV6Traffic|0040": {
            $sum: "$0040.IPV6Traffic"
        },
        "IPV6Traffic|0041": {
            $sum: "$0041.IPV6Traffic"
        },
        "IPV6Traffic|0042": {
            $sum: "$0042.IPV6Traffic"
        },
        "IPV6Traffic|0043": {
            $sum: "$0043.IPV6Traffic"
        },
        "IPV6Traffic|0044": {
            $sum: "$0044.IPV6Traffic"
        },
        "IPV6Traffic|0045": {
            $sum: "$0045.IPV6Traffic"
        },
        "IPV6Traffic|0046": {
            $sum: "$0046.IPV6Traffic"
        },
        "IPV6Traffic|0047": {
            $sum: "$0047.IPV6Traffic"
        },
        "IPV6Traffic|0048": {
            $sum: "$0048.IPV6Traffic"
        },
        "IPV6Traffic|0049": {
            $sum: "$0049.IPV6Traffic"
        },
        "IPV6Traffic|0050": {
            $sum: "$0050.IPV6Traffic"
        },
        "IPV6Traffic|0051": {
            $sum: "$0051.IPV6Traffic"
        },
        "IPV6Traffic|0052": {
            $sum: "$0052.IPV6Traffic"
        },
        "IPV6Traffic|0053": {
            $sum: "$0053.IPV6Traffic"
        },
        "IPV6Traffic|0054": {
            $sum: "$0054.IPV6Traffic"
        },
        "IPV6Traffic|0055": {
            $sum: "$0055.IPV6Traffic"
        },
        "IPV6Traffic|0056": {
            $sum: "$0056.IPV6Traffic"
        },
        "IPV6Traffic|0057": {
            $sum: "$0057.IPV6Traffic"
        },
        "IPV6Traffic|0058": {
            $sum: "$0058.IPV6Traffic"
        },
        "IPV6Traffic|0059": {
            $sum: "$0059.IPV6Traffic"
        },
        "IPV6Traffic|0100": {
            $sum: "$0100.IPV6Traffic"
        },
        "IPV6Traffic|0101": {
            $sum: "$0101.IPV6Traffic"
        },
        "IPV6Traffic|0102": {
            $sum: "$0102.IPV6Traffic"
        },
        "IPV6Traffic|0103": {
            $sum: "$0103.IPV6Traffic"
        },
        "IPV6Traffic|0104": {
            $sum: "$0104.IPV6Traffic"
        },
        "IPV6Traffic|0105": {
            $sum: "$0105.IPV6Traffic"
        },
        "IPV6Traffic|0106": {
            $sum: "$0106.IPV6Traffic"
        },
        "IPV6Traffic|0107": {
            $sum: "$0107.IPV6Traffic"
        },
        "IPV6Traffic|0108": {
            $sum: "$0108.IPV6Traffic"
        },
        "IPV6Traffic|0109": {
            $sum: "$0109.IPV6Traffic"
        },
        "IPV6Traffic|0110": {
            $sum: "$0110.IPV6Traffic"
        },
        "IPV6Traffic|0111": {
            $sum: "$0111.IPV6Traffic"
        },
        "IPV6Traffic|0112": {
            $sum: "$0112.IPV6Traffic"
        },
        "IPV6Traffic|0113": {
            $sum: "$0113.IPV6Traffic"
        },
        "IPV6Traffic|0114": {
            $sum: "$0114.IPV6Traffic"
        },
        "IPV6Traffic|0115": {
            $sum: "$0115.IPV6Traffic"
        },
        "IPV6Traffic|0116": {
            $sum: "$0116.IPV6Traffic"
        },
        "IPV6Traffic|0117": {
            $sum: "$0117.IPV6Traffic"
        },
        "IPV6Traffic|0118": {
            $sum: "$0118.IPV6Traffic"
        },
        "IPV6Traffic|0119": {
            $sum: "$0119.IPV6Traffic"
        },
        "IPV6Traffic|0120": {
            $sum: "$0120.IPV6Traffic"
        },
        "IPV6Traffic|0121": {
            $sum: "$0121.IPV6Traffic"
        },
        "IPV6Traffic|0122": {
            $sum: "$0122.IPV6Traffic"
        },
        "IPV6Traffic|0123": {
            $sum: "$0123.IPV6Traffic"
        },
        "IPV6Traffic|0124": {
            $sum: "$0124.IPV6Traffic"
        },
        "IPV6Traffic|0125": {
            $sum: "$0125.IPV6Traffic"
        },
        "IPV6Traffic|0126": {
            $sum: "$0126.IPV6Traffic"
        },
        "IPV6Traffic|0127": {
            $sum: "$0127.IPV6Traffic"
        },
        "IPV6Traffic|0128": {
            $sum: "$0128.IPV6Traffic"
        },
        "IPV6Traffic|0129": {
            $sum: "$0129.IPV6Traffic"
        },
        "IPV6Traffic|0130": {
            $sum: "$0130.IPV6Traffic"
        },
        "IPV6Traffic|0131": {
            $sum: "$0131.IPV6Traffic"
        },
        "IPV6Traffic|0132": {
            $sum: "$0132.IPV6Traffic"
        },
        "IPV6Traffic|0133": {
            $sum: "$0133.IPV6Traffic"
        },
        "IPV6Traffic|0134": {
            $sum: "$0134.IPV6Traffic"
        },
        "IPV6Traffic|0135": {
            $sum: "$0135.IPV6Traffic"
        },
        "IPV6Traffic|0136": {
            $sum: "$0136.IPV6Traffic"
        },
        "IPV6Traffic|0137": {
            $sum: "$0137.IPV6Traffic"
        },
        "IPV6Traffic|0138": {
            $sum: "$0138.IPV6Traffic"
        },
        "IPV6Traffic|0139": {
            $sum: "$0139.IPV6Traffic"
        },
        "IPV6Traffic|0140": {
            $sum: "$0140.IPV6Traffic"
        },
        "IPV6Traffic|0141": {
            $sum: "$0141.IPV6Traffic"
        },
        "IPV6Traffic|0142": {
            $sum: "$0142.IPV6Traffic"
        },
        "IPV6Traffic|0143": {
            $sum: "$0143.IPV6Traffic"
        },
        "IPV6Traffic|0144": {
            $sum: "$0144.IPV6Traffic"
        },
        "IPV6Traffic|0145": {
            $sum: "$0145.IPV6Traffic"
        },
        "IPV6Traffic|0146": {
            $sum: "$0146.IPV6Traffic"
        },
        "IPV6Traffic|0147": {
            $sum: "$0147.IPV6Traffic"
        },
        "IPV6Traffic|0148": {
            $sum: "$0148.IPV6Traffic"
        },
        "IPV6Traffic|0149": {
            $sum: "$0149.IPV6Traffic"
        },
        "IPV6Traffic|0150": {
            $sum: "$0150.IPV6Traffic"
        },
        "IPV6Traffic|0151": {
            $sum: "$0151.IPV6Traffic"
        },
        "IPV6Traffic|0152": {
            $sum: "$0152.IPV6Traffic"
        },
        "IPV6Traffic|0153": {
            $sum: "$0153.IPV6Traffic"
        },
        "IPV6Traffic|0154": {
            $sum: "$0154.IPV6Traffic"
        },
        "IPV6Traffic|0155": {
            $sum: "$0155.IPV6Traffic"
        },
        "IPV6Traffic|0156": {
            $sum: "$0156.IPV6Traffic"
        },
        "IPV6Traffic|0157": {
            $sum: "$0157.IPV6Traffic"
        },
        "IPV6Traffic|0158": {
            $sum: "$0158.IPV6Traffic"
        },
        "IPV6Traffic|0159": {
            $sum: "$0159.IPV6Traffic"
        },
        "IPV6Traffic|0200": {
            $sum: "$0200.IPV6Traffic"
        },
        "IPV6Traffic|0201": {
            $sum: "$0201.IPV6Traffic"
        },
        "IPV6Traffic|0202": {
            $sum: "$0202.IPV6Traffic"
        },
        "IPV6Traffic|0203": {
            $sum: "$0203.IPV6Traffic"
        },
        "IPV6Traffic|0204": {
            $sum: "$0204.IPV6Traffic"
        },
        "IPV6Traffic|0205": {
            $sum: "$0205.IPV6Traffic"
        },
        "IPV6Traffic|0206": {
            $sum: "$0206.IPV6Traffic"
        },
        "IPV6Traffic|0207": {
            $sum: "$0207.IPV6Traffic"
        },
        "IPV6Traffic|0208": {
            $sum: "$0208.IPV6Traffic"
        },
        "IPV6Traffic|0209": {
            $sum: "$0209.IPV6Traffic"
        },
        "IPV6Traffic|0210": {
            $sum: "$0210.IPV6Traffic"
        },
        "IPV6Traffic|0211": {
            $sum: "$0211.IPV6Traffic"
        },
        "IPV6Traffic|0212": {
            $sum: "$0212.IPV6Traffic"
        },
        "IPV6Traffic|0213": {
            $sum: "$0213.IPV6Traffic"
        },
        "IPV6Traffic|0214": {
            $sum: "$0214.IPV6Traffic"
        },
        "IPV6Traffic|0215": {
            $sum: "$0215.IPV6Traffic"
        },
        "IPV6Traffic|0216": {
            $sum: "$0216.IPV6Traffic"
        },
        "IPV6Traffic|0217": {
            $sum: "$0217.IPV6Traffic"
        },
        "IPV6Traffic|0218": {
            $sum: "$0218.IPV6Traffic"
        },
        "IPV6Traffic|0219": {
            $sum: "$0219.IPV6Traffic"
        },
        "IPV6Traffic|0220": {
            $sum: "$0220.IPV6Traffic"
        },
        "IPV6Traffic|0221": {
            $sum: "$0221.IPV6Traffic"
        },
        "IPV6Traffic|0222": {
            $sum: "$0222.IPV6Traffic"
        },
        "IPV6Traffic|0223": {
            $sum: "$0223.IPV6Traffic"
        },
        "IPV6Traffic|0224": {
            $sum: "$0224.IPV6Traffic"
        },
        "IPV6Traffic|0225": {
            $sum: "$0225.IPV6Traffic"
        },
        "IPV6Traffic|0226": {
            $sum: "$0226.IPV6Traffic"
        },
        "IPV6Traffic|0227": {
            $sum: "$0227.IPV6Traffic"
        },
        "IPV6Traffic|0228": {
            $sum: "$0228.IPV6Traffic"
        },
        "IPV6Traffic|0229": {
            $sum: "$0229.IPV6Traffic"
        },
        "IPV6Traffic|0230": {
            $sum: "$0230.IPV6Traffic"
        },
        "IPV6Traffic|0231": {
            $sum: "$0231.IPV6Traffic"
        },
        "IPV6Traffic|0232": {
            $sum: "$0232.IPV6Traffic"
        },
        "IPV6Traffic|0233": {
            $sum: "$0233.IPV6Traffic"
        },
        "IPV6Traffic|0234": {
            $sum: "$0234.IPV6Traffic"
        },
        "IPV6Traffic|0235": {
            $sum: "$0235.IPV6Traffic"
        },
        "IPV6Traffic|0236": {
            $sum: "$0236.IPV6Traffic"
        },
        "IPV6Traffic|0237": {
            $sum: "$0237.IPV6Traffic"
        },
        "IPV6Traffic|0238": {
            $sum: "$0238.IPV6Traffic"
        },
        "IPV6Traffic|0239": {
            $sum: "$0239.IPV6Traffic"
        },
        "IPV6Traffic|0240": {
            $sum: "$0240.IPV6Traffic"
        },
        "IPV6Traffic|0241": {
            $sum: "$0241.IPV6Traffic"
        },
        "IPV6Traffic|0242": {
            $sum: "$0242.IPV6Traffic"
        },
        "IPV6Traffic|0243": {
            $sum: "$0243.IPV6Traffic"
        },
        "IPV6Traffic|0244": {
            $sum: "$0244.IPV6Traffic"
        },
        "IPV6Traffic|0245": {
            $sum: "$0245.IPV6Traffic"
        },
        "IPV6Traffic|0246": {
            $sum: "$0246.IPV6Traffic"
        },
        "IPV6Traffic|0247": {
            $sum: "$0247.IPV6Traffic"
        },
        "IPV6Traffic|0248": {
            $sum: "$0248.IPV6Traffic"
        },
        "IPV6Traffic|0249": {
            $sum: "$0249.IPV6Traffic"
        },
        "IPV6Traffic|0250": {
            $sum: "$0250.IPV6Traffic"
        },
        "IPV6Traffic|0251": {
            $sum: "$0251.IPV6Traffic"
        },
        "IPV6Traffic|0252": {
            $sum: "$0252.IPV6Traffic"
        },
        "IPV6Traffic|0253": {
            $sum: "$0253.IPV6Traffic"
        },
        "IPV6Traffic|0254": {
            $sum: "$0254.IPV6Traffic"
        },
        "IPV6Traffic|0255": {
            $sum: "$0255.IPV6Traffic"
        },
        "IPV6Traffic|0256": {
            $sum: "$0256.IPV6Traffic"
        },
        "IPV6Traffic|0257": {
            $sum: "$0257.IPV6Traffic"
        },
        "IPV6Traffic|0258": {
            $sum: "$0258.IPV6Traffic"
        },
        "IPV6Traffic|0259": {
            $sum: "$0259.IPV6Traffic"
        },
        "IPV6Traffic|0300": {
            $sum: "$0300.IPV6Traffic"
        },
        "IPV6Traffic|0301": {
            $sum: "$0301.IPV6Traffic"
        },
        "IPV6Traffic|0302": {
            $sum: "$0302.IPV6Traffic"
        },
        "IPV6Traffic|0303": {
            $sum: "$0303.IPV6Traffic"
        },
        "IPV6Traffic|0304": {
            $sum: "$0304.IPV6Traffic"
        },
        "IPV6Traffic|0305": {
            $sum: "$0305.IPV6Traffic"
        },
        "IPV6Traffic|0306": {
            $sum: "$0306.IPV6Traffic"
        },
        "IPV6Traffic|0307": {
            $sum: "$0307.IPV6Traffic"
        },
        "IPV6Traffic|0308": {
            $sum: "$0308.IPV6Traffic"
        },
        "IPV6Traffic|0309": {
            $sum: "$0309.IPV6Traffic"
        },
        "IPV6Traffic|0310": {
            $sum: "$0310.IPV6Traffic"
        },
        "IPV6Traffic|0311": {
            $sum: "$0311.IPV6Traffic"
        },
        "IPV6Traffic|0312": {
            $sum: "$0312.IPV6Traffic"
        },
        "IPV6Traffic|0313": {
            $sum: "$0313.IPV6Traffic"
        },
        "IPV6Traffic|0314": {
            $sum: "$0314.IPV6Traffic"
        },
        "IPV6Traffic|0315": {
            $sum: "$0315.IPV6Traffic"
        },
        "IPV6Traffic|0316": {
            $sum: "$0316.IPV6Traffic"
        },
        "IPV6Traffic|0317": {
            $sum: "$0317.IPV6Traffic"
        },
        "IPV6Traffic|0318": {
            $sum: "$0318.IPV6Traffic"
        },
        "IPV6Traffic|0319": {
            $sum: "$0319.IPV6Traffic"
        },
        "IPV6Traffic|0320": {
            $sum: "$0320.IPV6Traffic"
        },
        "IPV6Traffic|0321": {
            $sum: "$0321.IPV6Traffic"
        },
        "IPV6Traffic|0322": {
            $sum: "$0322.IPV6Traffic"
        },
        "IPV6Traffic|0323": {
            $sum: "$0323.IPV6Traffic"
        },
        "IPV6Traffic|0324": {
            $sum: "$0324.IPV6Traffic"
        },
        "IPV6Traffic|0325": {
            $sum: "$0325.IPV6Traffic"
        },
        "IPV6Traffic|0326": {
            $sum: "$0326.IPV6Traffic"
        },
        "IPV6Traffic|0327": {
            $sum: "$0327.IPV6Traffic"
        },
        "IPV6Traffic|0328": {
            $sum: "$0328.IPV6Traffic"
        },
        "IPV6Traffic|0329": {
            $sum: "$0329.IPV6Traffic"
        },
        "IPV6Traffic|0330": {
            $sum: "$0330.IPV6Traffic"
        },
        "IPV6Traffic|0331": {
            $sum: "$0331.IPV6Traffic"
        },
        "IPV6Traffic|0332": {
            $sum: "$0332.IPV6Traffic"
        },
        "IPV6Traffic|0333": {
            $sum: "$0333.IPV6Traffic"
        },
        "IPV6Traffic|0334": {
            $sum: "$0334.IPV6Traffic"
        },
        "IPV6Traffic|0335": {
            $sum: "$0335.IPV6Traffic"
        },
        "IPV6Traffic|0336": {
            $sum: "$0336.IPV6Traffic"
        },
        "IPV6Traffic|0337": {
            $sum: "$0337.IPV6Traffic"
        },
        "IPV6Traffic|0338": {
            $sum: "$0338.IPV6Traffic"
        },
        "IPV6Traffic|0339": {
            $sum: "$0339.IPV6Traffic"
        },
        "IPV6Traffic|0340": {
            $sum: "$0340.IPV6Traffic"
        },
        "IPV6Traffic|0341": {
            $sum: "$0341.IPV6Traffic"
        },
        "IPV6Traffic|0342": {
            $sum: "$0342.IPV6Traffic"
        },
        "IPV6Traffic|0343": {
            $sum: "$0343.IPV6Traffic"
        },
        "IPV6Traffic|0344": {
            $sum: "$0344.IPV6Traffic"
        },
        "IPV6Traffic|0345": {
            $sum: "$0345.IPV6Traffic"
        },
        "IPV6Traffic|0346": {
            $sum: "$0346.IPV6Traffic"
        },
        "IPV6Traffic|0347": {
            $sum: "$0347.IPV6Traffic"
        },
        "IPV6Traffic|0348": {
            $sum: "$0348.IPV6Traffic"
        },
        "IPV6Traffic|0349": {
            $sum: "$0349.IPV6Traffic"
        },
        "IPV6Traffic|0350": {
            $sum: "$0350.IPV6Traffic"
        },
        "IPV6Traffic|0351": {
            $sum: "$0351.IPV6Traffic"
        },
        "IPV6Traffic|0352": {
            $sum: "$0352.IPV6Traffic"
        },
        "IPV6Traffic|0353": {
            $sum: "$0353.IPV6Traffic"
        },
        "IPV6Traffic|0354": {
            $sum: "$0354.IPV6Traffic"
        },
        "IPV6Traffic|0355": {
            $sum: "$0355.IPV6Traffic"
        },
        "IPV6Traffic|0356": {
            $sum: "$0356.IPV6Traffic"
        },
        "IPV6Traffic|0357": {
            $sum: "$0357.IPV6Traffic"
        },
        "IPV6Traffic|0358": {
            $sum: "$0358.IPV6Traffic"
        },
        "IPV6Traffic|0359": {
            $sum: "$0359.IPV6Traffic"
        },
        "IPV6Traffic|0400": {
            $sum: "$0400.IPV6Traffic"
        },
        "IPV6Traffic|0401": {
            $sum: "$0401.IPV6Traffic"
        },
        "IPV6Traffic|0402": {
            $sum: "$0402.IPV6Traffic"
        },
        "IPV6Traffic|0403": {
            $sum: "$0403.IPV6Traffic"
        },
        "IPV6Traffic|0404": {
            $sum: "$0404.IPV6Traffic"
        },
        "IPV6Traffic|0405": {
            $sum: "$0405.IPV6Traffic"
        },
        "IPV6Traffic|0406": {
            $sum: "$0406.IPV6Traffic"
        },
        "IPV6Traffic|0407": {
            $sum: "$0407.IPV6Traffic"
        },
        "IPV6Traffic|0408": {
            $sum: "$0408.IPV6Traffic"
        },
        "IPV6Traffic|0409": {
            $sum: "$0409.IPV6Traffic"
        },
        "IPV6Traffic|0410": {
            $sum: "$0410.IPV6Traffic"
        },
        "IPV6Traffic|0411": {
            $sum: "$0411.IPV6Traffic"
        },
        "IPV6Traffic|0412": {
            $sum: "$0412.IPV6Traffic"
        },
        "IPV6Traffic|0413": {
            $sum: "$0413.IPV6Traffic"
        },
        "IPV6Traffic|0414": {
            $sum: "$0414.IPV6Traffic"
        },
        "IPV6Traffic|0415": {
            $sum: "$0415.IPV6Traffic"
        },
        "IPV6Traffic|0416": {
            $sum: "$0416.IPV6Traffic"
        },
        "IPV6Traffic|0417": {
            $sum: "$0417.IPV6Traffic"
        },
        "IPV6Traffic|0418": {
            $sum: "$0418.IPV6Traffic"
        },
        "IPV6Traffic|0419": {
            $sum: "$0419.IPV6Traffic"
        },
        "IPV6Traffic|0420": {
            $sum: "$0420.IPV6Traffic"
        },
        "IPV6Traffic|0421": {
            $sum: "$0421.IPV6Traffic"
        },
        "IPV6Traffic|0422": {
            $sum: "$0422.IPV6Traffic"
        },
        "IPV6Traffic|0423": {
            $sum: "$0423.IPV6Traffic"
        },
        "IPV6Traffic|0424": {
            $sum: "$0424.IPV6Traffic"
        },
        "IPV6Traffic|0425": {
            $sum: "$0425.IPV6Traffic"
        },
        "IPV6Traffic|0426": {
            $sum: "$0426.IPV6Traffic"
        },
        "IPV6Traffic|0427": {
            $sum: "$0427.IPV6Traffic"
        },
        "IPV6Traffic|0428": {
            $sum: "$0428.IPV6Traffic"
        },
        "IPV6Traffic|0429": {
            $sum: "$0429.IPV6Traffic"
        },
        "IPV6Traffic|0430": {
            $sum: "$0430.IPV6Traffic"
        },
        "IPV6Traffic|0431": {
            $sum: "$0431.IPV6Traffic"
        },
        "IPV6Traffic|0432": {
            $sum: "$0432.IPV6Traffic"
        },
        "IPV6Traffic|0433": {
            $sum: "$0433.IPV6Traffic"
        },
        "IPV6Traffic|0434": {
            $sum: "$0434.IPV6Traffic"
        },
        "IPV6Traffic|0435": {
            $sum: "$0435.IPV6Traffic"
        },
        "IPV6Traffic|0436": {
            $sum: "$0436.IPV6Traffic"
        },
        "IPV6Traffic|0437": {
            $sum: "$0437.IPV6Traffic"
        },
        "IPV6Traffic|0438": {
            $sum: "$0438.IPV6Traffic"
        },
        "IPV6Traffic|0439": {
            $sum: "$0439.IPV6Traffic"
        },
        "IPV6Traffic|0440": {
            $sum: "$0440.IPV6Traffic"
        },
        "IPV6Traffic|0441": {
            $sum: "$0441.IPV6Traffic"
        },
        "IPV6Traffic|0442": {
            $sum: "$0442.IPV6Traffic"
        },
        "IPV6Traffic|0443": {
            $sum: "$0443.IPV6Traffic"
        },
        "IPV6Traffic|0444": {
            $sum: "$0444.IPV6Traffic"
        },
        "IPV6Traffic|0445": {
            $sum: "$0445.IPV6Traffic"
        },
        "IPV6Traffic|0446": {
            $sum: "$0446.IPV6Traffic"
        },
        "IPV6Traffic|0447": {
            $sum: "$0447.IPV6Traffic"
        },
        "IPV6Traffic|0448": {
            $sum: "$0448.IPV6Traffic"
        },
        "IPV6Traffic|0449": {
            $sum: "$0449.IPV6Traffic"
        },
        "IPV6Traffic|0450": {
            $sum: "$0450.IPV6Traffic"
        },
        "IPV6Traffic|0451": {
            $sum: "$0451.IPV6Traffic"
        },
        "IPV6Traffic|0452": {
            $sum: "$0452.IPV6Traffic"
        },
        "IPV6Traffic|0453": {
            $sum: "$0453.IPV6Traffic"
        },
        "IPV6Traffic|0454": {
            $sum: "$0454.IPV6Traffic"
        },
        "IPV6Traffic|0455": {
            $sum: "$0455.IPV6Traffic"
        },
        "IPV6Traffic|0456": {
            $sum: "$0456.IPV6Traffic"
        },
        "IPV6Traffic|0457": {
            $sum: "$0457.IPV6Traffic"
        },
        "IPV6Traffic|0458": {
            $sum: "$0458.IPV6Traffic"
        },
        "IPV6Traffic|0459": {
            $sum: "$0459.IPV6Traffic"
        },
        "IPV6Traffic|0500": {
            $sum: "$0500.IPV6Traffic"
        },
        "IPV6Traffic|0501": {
            $sum: "$0501.IPV6Traffic"
        },
        "IPV6Traffic|0502": {
            $sum: "$0502.IPV6Traffic"
        },
        "IPV6Traffic|0503": {
            $sum: "$0503.IPV6Traffic"
        },
        "IPV6Traffic|0504": {
            $sum: "$0504.IPV6Traffic"
        },
        "IPV6Traffic|0505": {
            $sum: "$0505.IPV6Traffic"
        },
        "IPV6Traffic|0506": {
            $sum: "$0506.IPV6Traffic"
        },
        "IPV6Traffic|0507": {
            $sum: "$0507.IPV6Traffic"
        },
        "IPV6Traffic|0508": {
            $sum: "$0508.IPV6Traffic"
        },
        "IPV6Traffic|0509": {
            $sum: "$0509.IPV6Traffic"
        },
        "IPV6Traffic|0510": {
            $sum: "$0510.IPV6Traffic"
        },
        "IPV6Traffic|0511": {
            $sum: "$0511.IPV6Traffic"
        },
        "IPV6Traffic|0512": {
            $sum: "$0512.IPV6Traffic"
        },
        "IPV6Traffic|0513": {
            $sum: "$0513.IPV6Traffic"
        },
        "IPV6Traffic|0514": {
            $sum: "$0514.IPV6Traffic"
        },
        "IPV6Traffic|0515": {
            $sum: "$0515.IPV6Traffic"
        },
        "IPV6Traffic|0516": {
            $sum: "$0516.IPV6Traffic"
        },
        "IPV6Traffic|0517": {
            $sum: "$0517.IPV6Traffic"
        },
        "IPV6Traffic|0518": {
            $sum: "$0518.IPV6Traffic"
        },
        "IPV6Traffic|0519": {
            $sum: "$0519.IPV6Traffic"
        },
        "IPV6Traffic|0520": {
            $sum: "$0520.IPV6Traffic"
        },
        "IPV6Traffic|0521": {
            $sum: "$0521.IPV6Traffic"
        },
        "IPV6Traffic|0522": {
            $sum: "$0522.IPV6Traffic"
        },
        "IPV6Traffic|0523": {
            $sum: "$0523.IPV6Traffic"
        },
        "IPV6Traffic|0524": {
            $sum: "$0524.IPV6Traffic"
        },
        "IPV6Traffic|0525": {
            $sum: "$0525.IPV6Traffic"
        },
        "IPV6Traffic|0526": {
            $sum: "$0526.IPV6Traffic"
        },
        "IPV6Traffic|0527": {
            $sum: "$0527.IPV6Traffic"
        },
        "IPV6Traffic|0528": {
            $sum: "$0528.IPV6Traffic"
        },
        "IPV6Traffic|0529": {
            $sum: "$0529.IPV6Traffic"
        },
        "IPV6Traffic|0530": {
            $sum: "$0530.IPV6Traffic"
        },
        "IPV6Traffic|0531": {
            $sum: "$0531.IPV6Traffic"
        },
        "IPV6Traffic|0532": {
            $sum: "$0532.IPV6Traffic"
        },
        "IPV6Traffic|0533": {
            $sum: "$0533.IPV6Traffic"
        },
        "IPV6Traffic|0534": {
            $sum: "$0534.IPV6Traffic"
        },
        "IPV6Traffic|0535": {
            $sum: "$0535.IPV6Traffic"
        },
        "IPV6Traffic|0536": {
            $sum: "$0536.IPV6Traffic"
        },
        "IPV6Traffic|0537": {
            $sum: "$0537.IPV6Traffic"
        },
        "IPV6Traffic|0538": {
            $sum: "$0538.IPV6Traffic"
        },
        "IPV6Traffic|0539": {
            $sum: "$0539.IPV6Traffic"
        },
        "IPV6Traffic|0540": {
            $sum: "$0540.IPV6Traffic"
        },
        "IPV6Traffic|0541": {
            $sum: "$0541.IPV6Traffic"
        },
        "IPV6Traffic|0542": {
            $sum: "$0542.IPV6Traffic"
        },
        "IPV6Traffic|0543": {
            $sum: "$0543.IPV6Traffic"
        },
        "IPV6Traffic|0544": {
            $sum: "$0544.IPV6Traffic"
        },
        "IPV6Traffic|0545": {
            $sum: "$0545.IPV6Traffic"
        },
        "IPV6Traffic|0546": {
            $sum: "$0546.IPV6Traffic"
        },
        "IPV6Traffic|0547": {
            $sum: "$0547.IPV6Traffic"
        },
        "IPV6Traffic|0548": {
            $sum: "$0548.IPV6Traffic"
        },
        "IPV6Traffic|0549": {
            $sum: "$0549.IPV6Traffic"
        },
        "IPV6Traffic|0550": {
            $sum: "$0550.IPV6Traffic"
        },
        "IPV6Traffic|0551": {
            $sum: "$0551.IPV6Traffic"
        },
        "IPV6Traffic|0552": {
            $sum: "$0552.IPV6Traffic"
        },
        "IPV6Traffic|0553": {
            $sum: "$0553.IPV6Traffic"
        },
        "IPV6Traffic|0554": {
            $sum: "$0554.IPV6Traffic"
        },
        "IPV6Traffic|0555": {
            $sum: "$0555.IPV6Traffic"
        },
        "IPV6Traffic|0556": {
            $sum: "$0556.IPV6Traffic"
        },
        "IPV6Traffic|0557": {
            $sum: "$0557.IPV6Traffic"
        },
        "IPV6Traffic|0558": {
            $sum: "$0558.IPV6Traffic"
        },
        "IPV6Traffic|0559": {
            $sum: "$0559.IPV6Traffic"
        },
        "IPV6Traffic|0600": {
            $sum: "$0600.IPV6Traffic"
        },
        "IPV6Traffic|0601": {
            $sum: "$0601.IPV6Traffic"
        },
        "IPV6Traffic|0602": {
            $sum: "$0602.IPV6Traffic"
        },
        "IPV6Traffic|0603": {
            $sum: "$0603.IPV6Traffic"
        },
        "IPV6Traffic|0604": {
            $sum: "$0604.IPV6Traffic"
        },
        "IPV6Traffic|0605": {
            $sum: "$0605.IPV6Traffic"
        },
        "IPV6Traffic|0606": {
            $sum: "$0606.IPV6Traffic"
        },
        "IPV6Traffic|0607": {
            $sum: "$0607.IPV6Traffic"
        },
        "IPV6Traffic|0608": {
            $sum: "$0608.IPV6Traffic"
        },
        "IPV6Traffic|0609": {
            $sum: "$0609.IPV6Traffic"
        },
        "IPV6Traffic|0610": {
            $sum: "$0610.IPV6Traffic"
        },
        "IPV6Traffic|0611": {
            $sum: "$0611.IPV6Traffic"
        },
        "IPV6Traffic|0612": {
            $sum: "$0612.IPV6Traffic"
        },
        "IPV6Traffic|0613": {
            $sum: "$0613.IPV6Traffic"
        },
        "IPV6Traffic|0614": {
            $sum: "$0614.IPV6Traffic"
        },
        "IPV6Traffic|0615": {
            $sum: "$0615.IPV6Traffic"
        },
        "IPV6Traffic|0616": {
            $sum: "$0616.IPV6Traffic"
        },
        "IPV6Traffic|0617": {
            $sum: "$0617.IPV6Traffic"
        },
        "IPV6Traffic|0618": {
            $sum: "$0618.IPV6Traffic"
        },
        "IPV6Traffic|0619": {
            $sum: "$0619.IPV6Traffic"
        },
        "IPV6Traffic|0620": {
            $sum: "$0620.IPV6Traffic"
        },
        "IPV6Traffic|0621": {
            $sum: "$0621.IPV6Traffic"
        },
        "IPV6Traffic|0622": {
            $sum: "$0622.IPV6Traffic"
        },
        "IPV6Traffic|0623": {
            $sum: "$0623.IPV6Traffic"
        },
        "IPV6Traffic|0624": {
            $sum: "$0624.IPV6Traffic"
        },
        "IPV6Traffic|0625": {
            $sum: "$0625.IPV6Traffic"
        },
        "IPV6Traffic|0626": {
            $sum: "$0626.IPV6Traffic"
        },
        "IPV6Traffic|0627": {
            $sum: "$0627.IPV6Traffic"
        },
        "IPV6Traffic|0628": {
            $sum: "$0628.IPV6Traffic"
        },
        "IPV6Traffic|0629": {
            $sum: "$0629.IPV6Traffic"
        },
        "IPV6Traffic|0630": {
            $sum: "$0630.IPV6Traffic"
        },
        "IPV6Traffic|0631": {
            $sum: "$0631.IPV6Traffic"
        },
        "IPV6Traffic|0632": {
            $sum: "$0632.IPV6Traffic"
        },
        "IPV6Traffic|0633": {
            $sum: "$0633.IPV6Traffic"
        },
        "IPV6Traffic|0634": {
            $sum: "$0634.IPV6Traffic"
        },
        "IPV6Traffic|0635": {
            $sum: "$0635.IPV6Traffic"
        },
        "IPV6Traffic|0636": {
            $sum: "$0636.IPV6Traffic"
        },
        "IPV6Traffic|0637": {
            $sum: "$0637.IPV6Traffic"
        },
        "IPV6Traffic|0638": {
            $sum: "$0638.IPV6Traffic"
        },
        "IPV6Traffic|0639": {
            $sum: "$0639.IPV6Traffic"
        },
        "IPV6Traffic|0640": {
            $sum: "$0640.IPV6Traffic"
        },
        "IPV6Traffic|0641": {
            $sum: "$0641.IPV6Traffic"
        },
        "IPV6Traffic|0642": {
            $sum: "$0642.IPV6Traffic"
        },
        "IPV6Traffic|0643": {
            $sum: "$0643.IPV6Traffic"
        },
        "IPV6Traffic|0644": {
            $sum: "$0644.IPV6Traffic"
        },
        "IPV6Traffic|0645": {
            $sum: "$0645.IPV6Traffic"
        },
        "IPV6Traffic|0646": {
            $sum: "$0646.IPV6Traffic"
        },
        "IPV6Traffic|0647": {
            $sum: "$0647.IPV6Traffic"
        },
        "IPV6Traffic|0648": {
            $sum: "$0648.IPV6Traffic"
        },
        "IPV6Traffic|0649": {
            $sum: "$0649.IPV6Traffic"
        },
        "IPV6Traffic|0650": {
            $sum: "$0650.IPV6Traffic"
        },
        "IPV6Traffic|0651": {
            $sum: "$0651.IPV6Traffic"
        },
        "IPV6Traffic|0652": {
            $sum: "$0652.IPV6Traffic"
        },
        "IPV6Traffic|0653": {
            $sum: "$0653.IPV6Traffic"
        },
        "IPV6Traffic|0654": {
            $sum: "$0654.IPV6Traffic"
        },
        "IPV6Traffic|0655": {
            $sum: "$0655.IPV6Traffic"
        },
        "IPV6Traffic|0656": {
            $sum: "$0656.IPV6Traffic"
        },
        "IPV6Traffic|0657": {
            $sum: "$0657.IPV6Traffic"
        },
        "IPV6Traffic|0658": {
            $sum: "$0658.IPV6Traffic"
        },
        "IPV6Traffic|0659": {
            $sum: "$0659.IPV6Traffic"
        },
        "IPV6Traffic|0700": {
            $sum: "$0700.IPV6Traffic"
        },
        "IPV6Traffic|0701": {
            $sum: "$0701.IPV6Traffic"
        },
        "IPV6Traffic|0702": {
            $sum: "$0702.IPV6Traffic"
        },
        "IPV6Traffic|0703": {
            $sum: "$0703.IPV6Traffic"
        },
        "IPV6Traffic|0704": {
            $sum: "$0704.IPV6Traffic"
        },
        "IPV6Traffic|0705": {
            $sum: "$0705.IPV6Traffic"
        },
        "IPV6Traffic|0706": {
            $sum: "$0706.IPV6Traffic"
        },
        "IPV6Traffic|0707": {
            $sum: "$0707.IPV6Traffic"
        },
        "IPV6Traffic|0708": {
            $sum: "$0708.IPV6Traffic"
        },
        "IPV6Traffic|0709": {
            $sum: "$0709.IPV6Traffic"
        },
        "IPV6Traffic|0710": {
            $sum: "$0710.IPV6Traffic"
        },
        "IPV6Traffic|0711": {
            $sum: "$0711.IPV6Traffic"
        },
        "IPV6Traffic|0712": {
            $sum: "$0712.IPV6Traffic"
        },
        "IPV6Traffic|0713": {
            $sum: "$0713.IPV6Traffic"
        },
        "IPV6Traffic|0714": {
            $sum: "$0714.IPV6Traffic"
        },
        "IPV6Traffic|0715": {
            $sum: "$0715.IPV6Traffic"
        },
        "IPV6Traffic|0716": {
            $sum: "$0716.IPV6Traffic"
        },
        "IPV6Traffic|0717": {
            $sum: "$0717.IPV6Traffic"
        },
        "IPV6Traffic|0718": {
            $sum: "$0718.IPV6Traffic"
        },
        "IPV6Traffic|0719": {
            $sum: "$0719.IPV6Traffic"
        },
        "IPV6Traffic|0720": {
            $sum: "$0720.IPV6Traffic"
        },
        "IPV6Traffic|0721": {
            $sum: "$0721.IPV6Traffic"
        },
        "IPV6Traffic|0722": {
            $sum: "$0722.IPV6Traffic"
        },
        "IPV6Traffic|0723": {
            $sum: "$0723.IPV6Traffic"
        },
        "IPV6Traffic|0724": {
            $sum: "$0724.IPV6Traffic"
        },
        "IPV6Traffic|0725": {
            $sum: "$0725.IPV6Traffic"
        },
        "IPV6Traffic|0726": {
            $sum: "$0726.IPV6Traffic"
        },
        "IPV6Traffic|0727": {
            $sum: "$0727.IPV6Traffic"
        },
        "IPV6Traffic|0728": {
            $sum: "$0728.IPV6Traffic"
        },
        "IPV6Traffic|0729": {
            $sum: "$0729.IPV6Traffic"
        },
        "IPV6Traffic|0730": {
            $sum: "$0730.IPV6Traffic"
        },
        "IPV6Traffic|0731": {
            $sum: "$0731.IPV6Traffic"
        },
        "IPV6Traffic|0732": {
            $sum: "$0732.IPV6Traffic"
        },
        "IPV6Traffic|0733": {
            $sum: "$0733.IPV6Traffic"
        },
        "IPV6Traffic|0734": {
            $sum: "$0734.IPV6Traffic"
        },
        "IPV6Traffic|0735": {
            $sum: "$0735.IPV6Traffic"
        },
        "IPV6Traffic|0736": {
            $sum: "$0736.IPV6Traffic"
        },
        "IPV6Traffic|0737": {
            $sum: "$0737.IPV6Traffic"
        },
        "IPV6Traffic|0738": {
            $sum: "$0738.IPV6Traffic"
        },
        "IPV6Traffic|0739": {
            $sum: "$0739.IPV6Traffic"
        },
        "IPV6Traffic|0740": {
            $sum: "$0740.IPV6Traffic"
        },
        "IPV6Traffic|0741": {
            $sum: "$0741.IPV6Traffic"
        },
        "IPV6Traffic|0742": {
            $sum: "$0742.IPV6Traffic"
        },
        "IPV6Traffic|0743": {
            $sum: "$0743.IPV6Traffic"
        },
        "IPV6Traffic|0744": {
            $sum: "$0744.IPV6Traffic"
        },
        "IPV6Traffic|0745": {
            $sum: "$0745.IPV6Traffic"
        },
        "IPV6Traffic|0746": {
            $sum: "$0746.IPV6Traffic"
        },
        "IPV6Traffic|0747": {
            $sum: "$0747.IPV6Traffic"
        },
        "IPV6Traffic|0748": {
            $sum: "$0748.IPV6Traffic"
        },
        "IPV6Traffic|0749": {
            $sum: "$0749.IPV6Traffic"
        },
        "IPV6Traffic|0750": {
            $sum: "$0750.IPV6Traffic"
        },
        "IPV6Traffic|0751": {
            $sum: "$0751.IPV6Traffic"
        },
        "IPV6Traffic|0752": {
            $sum: "$0752.IPV6Traffic"
        },
        "IPV6Traffic|0753": {
            $sum: "$0753.IPV6Traffic"
        },
        "IPV6Traffic|0754": {
            $sum: "$0754.IPV6Traffic"
        },
        "IPV6Traffic|0755": {
            $sum: "$0755.IPV6Traffic"
        },
        "IPV6Traffic|0756": {
            $sum: "$0756.IPV6Traffic"
        },
        "IPV6Traffic|0757": {
            $sum: "$0757.IPV6Traffic"
        },
        "IPV6Traffic|0758": {
            $sum: "$0758.IPV6Traffic"
        },
        "IPV6Traffic|0759": {
            $sum: "$0759.IPV6Traffic"
        },
        "IPV6Traffic|0800": {
            $sum: "$0800.IPV6Traffic"
        },
        "IPV6Traffic|0801": {
            $sum: "$0801.IPV6Traffic"
        },
        "IPV6Traffic|0802": {
            $sum: "$0802.IPV6Traffic"
        },
        "IPV6Traffic|0803": {
            $sum: "$0803.IPV6Traffic"
        },
        "IPV6Traffic|0804": {
            $sum: "$0804.IPV6Traffic"
        },
        "IPV6Traffic|0805": {
            $sum: "$0805.IPV6Traffic"
        },
        "IPV6Traffic|0806": {
            $sum: "$0806.IPV6Traffic"
        },
        "IPV6Traffic|0807": {
            $sum: "$0807.IPV6Traffic"
        },
        "IPV6Traffic|0808": {
            $sum: "$0808.IPV6Traffic"
        },
        "IPV6Traffic|0809": {
            $sum: "$0809.IPV6Traffic"
        },
        "IPV6Traffic|0810": {
            $sum: "$0810.IPV6Traffic"
        },
        "IPV6Traffic|0811": {
            $sum: "$0811.IPV6Traffic"
        },
        "IPV6Traffic|0812": {
            $sum: "$0812.IPV6Traffic"
        },
        "IPV6Traffic|0813": {
            $sum: "$0813.IPV6Traffic"
        },
        "IPV6Traffic|0814": {
            $sum: "$0814.IPV6Traffic"
        },
        "IPV6Traffic|0815": {
            $sum: "$0815.IPV6Traffic"
        },
        "IPV6Traffic|0816": {
            $sum: "$0816.IPV6Traffic"
        },
        "IPV6Traffic|0817": {
            $sum: "$0817.IPV6Traffic"
        },
        "IPV6Traffic|0818": {
            $sum: "$0818.IPV6Traffic"
        },
        "IPV6Traffic|0819": {
            $sum: "$0819.IPV6Traffic"
        },
        "IPV6Traffic|0820": {
            $sum: "$0820.IPV6Traffic"
        },
        "IPV6Traffic|0821": {
            $sum: "$0821.IPV6Traffic"
        },
        "IPV6Traffic|0822": {
            $sum: "$0822.IPV6Traffic"
        },
        "IPV6Traffic|0823": {
            $sum: "$0823.IPV6Traffic"
        },
        "IPV6Traffic|0824": {
            $sum: "$0824.IPV6Traffic"
        },
        "IPV6Traffic|0825": {
            $sum: "$0825.IPV6Traffic"
        },
        "IPV6Traffic|0826": {
            $sum: "$0826.IPV6Traffic"
        },
        "IPV6Traffic|0827": {
            $sum: "$0827.IPV6Traffic"
        },
        "IPV6Traffic|0828": {
            $sum: "$0828.IPV6Traffic"
        },
        "IPV6Traffic|0829": {
            $sum: "$0829.IPV6Traffic"
        },
        "IPV6Traffic|0830": {
            $sum: "$0830.IPV6Traffic"
        },
        "IPV6Traffic|0831": {
            $sum: "$0831.IPV6Traffic"
        },
        "IPV6Traffic|0832": {
            $sum: "$0832.IPV6Traffic"
        },
        "IPV6Traffic|0833": {
            $sum: "$0833.IPV6Traffic"
        },
        "IPV6Traffic|0834": {
            $sum: "$0834.IPV6Traffic"
        },
        "IPV6Traffic|0835": {
            $sum: "$0835.IPV6Traffic"
        },
        "IPV6Traffic|0836": {
            $sum: "$0836.IPV6Traffic"
        },
        "IPV6Traffic|0837": {
            $sum: "$0837.IPV6Traffic"
        },
        "IPV6Traffic|0838": {
            $sum: "$0838.IPV6Traffic"
        },
        "IPV6Traffic|0839": {
            $sum: "$0839.IPV6Traffic"
        },
        "IPV6Traffic|0840": {
            $sum: "$0840.IPV6Traffic"
        },
        "IPV6Traffic|0841": {
            $sum: "$0841.IPV6Traffic"
        },
        "IPV6Traffic|0842": {
            $sum: "$0842.IPV6Traffic"
        },
        "IPV6Traffic|0843": {
            $sum: "$0843.IPV6Traffic"
        },
        "IPV6Traffic|0844": {
            $sum: "$0844.IPV6Traffic"
        },
        "IPV6Traffic|0845": {
            $sum: "$0845.IPV6Traffic"
        },
        "IPV6Traffic|0846": {
            $sum: "$0846.IPV6Traffic"
        },
        "IPV6Traffic|0847": {
            $sum: "$0847.IPV6Traffic"
        },
        "IPV6Traffic|0848": {
            $sum: "$0848.IPV6Traffic"
        },
        "IPV6Traffic|0849": {
            $sum: "$0849.IPV6Traffic"
        },
        "IPV6Traffic|0850": {
            $sum: "$0850.IPV6Traffic"
        },
        "IPV6Traffic|0851": {
            $sum: "$0851.IPV6Traffic"
        },
        "IPV6Traffic|0852": {
            $sum: "$0852.IPV6Traffic"
        },
        "IPV6Traffic|0853": {
            $sum: "$0853.IPV6Traffic"
        },
        "IPV6Traffic|0854": {
            $sum: "$0854.IPV6Traffic"
        },
        "IPV6Traffic|0855": {
            $sum: "$0855.IPV6Traffic"
        },
        "IPV6Traffic|0856": {
            $sum: "$0856.IPV6Traffic"
        },
        "IPV6Traffic|0857": {
            $sum: "$0857.IPV6Traffic"
        },
        "IPV6Traffic|0858": {
            $sum: "$0858.IPV6Traffic"
        },
        "IPV6Traffic|0859": {
            $sum: "$0859.IPV6Traffic"
        },
        "IPV6Traffic|0900": {
            $sum: "$0900.IPV6Traffic"
        },
        "IPV6Traffic|0901": {
            $sum: "$0901.IPV6Traffic"
        },
        "IPV6Traffic|0902": {
            $sum: "$0902.IPV6Traffic"
        },
        "IPV6Traffic|0903": {
            $sum: "$0903.IPV6Traffic"
        },
        "IPV6Traffic|0904": {
            $sum: "$0904.IPV6Traffic"
        },
        "IPV6Traffic|0905": {
            $sum: "$0905.IPV6Traffic"
        },
        "IPV6Traffic|0906": {
            $sum: "$0906.IPV6Traffic"
        },
        "IPV6Traffic|0907": {
            $sum: "$0907.IPV6Traffic"
        },
        "IPV6Traffic|0908": {
            $sum: "$0908.IPV6Traffic"
        },
        "IPV6Traffic|0909": {
            $sum: "$0909.IPV6Traffic"
        },
        "IPV6Traffic|0910": {
            $sum: "$0910.IPV6Traffic"
        },
        "IPV6Traffic|0911": {
            $sum: "$0911.IPV6Traffic"
        },
        "IPV6Traffic|0912": {
            $sum: "$0912.IPV6Traffic"
        },
        "IPV6Traffic|0913": {
            $sum: "$0913.IPV6Traffic"
        },
        "IPV6Traffic|0914": {
            $sum: "$0914.IPV6Traffic"
        },
        "IPV6Traffic|0915": {
            $sum: "$0915.IPV6Traffic"
        },
        "IPV6Traffic|0916": {
            $sum: "$0916.IPV6Traffic"
        },
        "IPV6Traffic|0917": {
            $sum: "$0917.IPV6Traffic"
        },
        "IPV6Traffic|0918": {
            $sum: "$0918.IPV6Traffic"
        },
        "IPV6Traffic|0919": {
            $sum: "$0919.IPV6Traffic"
        },
        "IPV6Traffic|0920": {
            $sum: "$0920.IPV6Traffic"
        },
        "IPV6Traffic|0921": {
            $sum: "$0921.IPV6Traffic"
        },
        "IPV6Traffic|0922": {
            $sum: "$0922.IPV6Traffic"
        },
        "IPV6Traffic|0923": {
            $sum: "$0923.IPV6Traffic"
        },
        "IPV6Traffic|0924": {
            $sum: "$0924.IPV6Traffic"
        },
        "IPV6Traffic|0925": {
            $sum: "$0925.IPV6Traffic"
        },
        "IPV6Traffic|0926": {
            $sum: "$0926.IPV6Traffic"
        },
        "IPV6Traffic|0927": {
            $sum: "$0927.IPV6Traffic"
        },
        "IPV6Traffic|0928": {
            $sum: "$0928.IPV6Traffic"
        },
        "IPV6Traffic|0929": {
            $sum: "$0929.IPV6Traffic"
        },
        "IPV6Traffic|0930": {
            $sum: "$0930.IPV6Traffic"
        },
        "IPV6Traffic|0931": {
            $sum: "$0931.IPV6Traffic"
        },
        "IPV6Traffic|0932": {
            $sum: "$0932.IPV6Traffic"
        },
        "IPV6Traffic|0933": {
            $sum: "$0933.IPV6Traffic"
        },
        "IPV6Traffic|0934": {
            $sum: "$0934.IPV6Traffic"
        },
        "IPV6Traffic|0935": {
            $sum: "$0935.IPV6Traffic"
        },
        "IPV6Traffic|0936": {
            $sum: "$0936.IPV6Traffic"
        },
        "IPV6Traffic|0937": {
            $sum: "$0937.IPV6Traffic"
        },
        "IPV6Traffic|0938": {
            $sum: "$0938.IPV6Traffic"
        },
        "IPV6Traffic|0939": {
            $sum: "$0939.IPV6Traffic"
        },
        "IPV6Traffic|0940": {
            $sum: "$0940.IPV6Traffic"
        },
        "IPV6Traffic|0941": {
            $sum: "$0941.IPV6Traffic"
        },
        "IPV6Traffic|0942": {
            $sum: "$0942.IPV6Traffic"
        },
        "IPV6Traffic|0943": {
            $sum: "$0943.IPV6Traffic"
        },
        "IPV6Traffic|0944": {
            $sum: "$0944.IPV6Traffic"
        },
        "IPV6Traffic|0945": {
            $sum: "$0945.IPV6Traffic"
        },
        "IPV6Traffic|0946": {
            $sum: "$0946.IPV6Traffic"
        },
        "IPV6Traffic|0947": {
            $sum: "$0947.IPV6Traffic"
        },
        "IPV6Traffic|0948": {
            $sum: "$0948.IPV6Traffic"
        },
        "IPV6Traffic|0949": {
            $sum: "$0949.IPV6Traffic"
        },
        "IPV6Traffic|0950": {
            $sum: "$0950.IPV6Traffic"
        },
        "IPV6Traffic|0951": {
            $sum: "$0951.IPV6Traffic"
        },
        "IPV6Traffic|0952": {
            $sum: "$0952.IPV6Traffic"
        },
        "IPV6Traffic|0953": {
            $sum: "$0953.IPV6Traffic"
        },
        "IPV6Traffic|0954": {
            $sum: "$0954.IPV6Traffic"
        },
        "IPV6Traffic|0955": {
            $sum: "$0955.IPV6Traffic"
        },
        "IPV6Traffic|0956": {
            $sum: "$0956.IPV6Traffic"
        },
        "IPV6Traffic|0957": {
            $sum: "$0957.IPV6Traffic"
        },
        "IPV6Traffic|0958": {
            $sum: "$0958.IPV6Traffic"
        },
        "IPV6Traffic|0959": {
            $sum: "$0959.IPV6Traffic"
        },
        "IPV6Traffic|1000": {
            $sum: "$1000.IPV6Traffic"
        },
        "IPV6Traffic|1001": {
            $sum: "$1001.IPV6Traffic"
        },
        "IPV6Traffic|1002": {
            $sum: "$1002.IPV6Traffic"
        },
        "IPV6Traffic|1003": {
            $sum: "$1003.IPV6Traffic"
        },
        "IPV6Traffic|1004": {
            $sum: "$1004.IPV6Traffic"
        },
        "IPV6Traffic|1005": {
            $sum: "$1005.IPV6Traffic"
        },
        "IPV6Traffic|1006": {
            $sum: "$1006.IPV6Traffic"
        },
        "IPV6Traffic|1007": {
            $sum: "$1007.IPV6Traffic"
        },
        "IPV6Traffic|1008": {
            $sum: "$1008.IPV6Traffic"
        },
        "IPV6Traffic|1009": {
            $sum: "$1009.IPV6Traffic"
        },
        "IPV6Traffic|1010": {
            $sum: "$1010.IPV6Traffic"
        },
        "IPV6Traffic|1011": {
            $sum: "$1011.IPV6Traffic"
        },
        "IPV6Traffic|1012": {
            $sum: "$1012.IPV6Traffic"
        },
        "IPV6Traffic|1013": {
            $sum: "$1013.IPV6Traffic"
        },
        "IPV6Traffic|1014": {
            $sum: "$1014.IPV6Traffic"
        },
        "IPV6Traffic|1015": {
            $sum: "$1015.IPV6Traffic"
        },
        "IPV6Traffic|1016": {
            $sum: "$1016.IPV6Traffic"
        },
        "IPV6Traffic|1017": {
            $sum: "$1017.IPV6Traffic"
        },
        "IPV6Traffic|1018": {
            $sum: "$1018.IPV6Traffic"
        },
        "IPV6Traffic|1019": {
            $sum: "$1019.IPV6Traffic"
        },
        "IPV6Traffic|1020": {
            $sum: "$1020.IPV6Traffic"
        },
        "IPV6Traffic|1021": {
            $sum: "$1021.IPV6Traffic"
        },
        "IPV6Traffic|1022": {
            $sum: "$1022.IPV6Traffic"
        },
        "IPV6Traffic|1023": {
            $sum: "$1023.IPV6Traffic"
        },
        "IPV6Traffic|1024": {
            $sum: "$1024.IPV6Traffic"
        },
        "IPV6Traffic|1025": {
            $sum: "$1025.IPV6Traffic"
        },
        "IPV6Traffic|1026": {
            $sum: "$1026.IPV6Traffic"
        },
        "IPV6Traffic|1027": {
            $sum: "$1027.IPV6Traffic"
        },
        "IPV6Traffic|1028": {
            $sum: "$1028.IPV6Traffic"
        },
        "IPV6Traffic|1029": {
            $sum: "$1029.IPV6Traffic"
        },
        "IPV6Traffic|1030": {
            $sum: "$1030.IPV6Traffic"
        },
        "IPV6Traffic|1031": {
            $sum: "$1031.IPV6Traffic"
        },
        "IPV6Traffic|1032": {
            $sum: "$1032.IPV6Traffic"
        },
        "IPV6Traffic|1033": {
            $sum: "$1033.IPV6Traffic"
        },
        "IPV6Traffic|1034": {
            $sum: "$1034.IPV6Traffic"
        },
        "IPV6Traffic|1035": {
            $sum: "$1035.IPV6Traffic"
        },
        "IPV6Traffic|1036": {
            $sum: "$1036.IPV6Traffic"
        },
        "IPV6Traffic|1037": {
            $sum: "$1037.IPV6Traffic"
        },
        "IPV6Traffic|1038": {
            $sum: "$1038.IPV6Traffic"
        },
        "IPV6Traffic|1039": {
            $sum: "$1039.IPV6Traffic"
        },
        "IPV6Traffic|1040": {
            $sum: "$1040.IPV6Traffic"
        },
        "IPV6Traffic|1041": {
            $sum: "$1041.IPV6Traffic"
        },
        "IPV6Traffic|1042": {
            $sum: "$1042.IPV6Traffic"
        },
        "IPV6Traffic|1043": {
            $sum: "$1043.IPV6Traffic"
        },
        "IPV6Traffic|1044": {
            $sum: "$1044.IPV6Traffic"
        },
        "IPV6Traffic|1045": {
            $sum: "$1045.IPV6Traffic"
        },
        "IPV6Traffic|1046": {
            $sum: "$1046.IPV6Traffic"
        },
        "IPV6Traffic|1047": {
            $sum: "$1047.IPV6Traffic"
        },
        "IPV6Traffic|1048": {
            $sum: "$1048.IPV6Traffic"
        },
        "IPV6Traffic|1049": {
            $sum: "$1049.IPV6Traffic"
        },
        "IPV6Traffic|1050": {
            $sum: "$1050.IPV6Traffic"
        },
        "IPV6Traffic|1051": {
            $sum: "$1051.IPV6Traffic"
        },
        "IPV6Traffic|1052": {
            $sum: "$1052.IPV6Traffic"
        },
        "IPV6Traffic|1053": {
            $sum: "$1053.IPV6Traffic"
        },
        "IPV6Traffic|1054": {
            $sum: "$1054.IPV6Traffic"
        },
        "IPV6Traffic|1055": {
            $sum: "$1055.IPV6Traffic"
        },
        "IPV6Traffic|1056": {
            $sum: "$1056.IPV6Traffic"
        },
        "IPV6Traffic|1057": {
            $sum: "$1057.IPV6Traffic"
        },
        "IPV6Traffic|1058": {
            $sum: "$1058.IPV6Traffic"
        },
        "IPV6Traffic|1059": {
            $sum: "$1059.IPV6Traffic"
        },
        "IPV6Traffic|1100": {
            $sum: "$1100.IPV6Traffic"
        },
        "IPV6Traffic|1101": {
            $sum: "$1101.IPV6Traffic"
        },
        "IPV6Traffic|1102": {
            $sum: "$1102.IPV6Traffic"
        },
        "IPV6Traffic|1103": {
            $sum: "$1103.IPV6Traffic"
        },
        "IPV6Traffic|1104": {
            $sum: "$1104.IPV6Traffic"
        },
        "IPV6Traffic|1105": {
            $sum: "$1105.IPV6Traffic"
        },
        "IPV6Traffic|1106": {
            $sum: "$1106.IPV6Traffic"
        },
        "IPV6Traffic|1107": {
            $sum: "$1107.IPV6Traffic"
        },
        "IPV6Traffic|1108": {
            $sum: "$1108.IPV6Traffic"
        },
        "IPV6Traffic|1109": {
            $sum: "$1109.IPV6Traffic"
        },
        "IPV6Traffic|1110": {
            $sum: "$1110.IPV6Traffic"
        },
        "IPV6Traffic|1111": {
            $sum: "$1111.IPV6Traffic"
        },
        "IPV6Traffic|1112": {
            $sum: "$1112.IPV6Traffic"
        },
        "IPV6Traffic|1113": {
            $sum: "$1113.IPV6Traffic"
        },
        "IPV6Traffic|1114": {
            $sum: "$1114.IPV6Traffic"
        },
        "IPV6Traffic|1115": {
            $sum: "$1115.IPV6Traffic"
        },
        "IPV6Traffic|1116": {
            $sum: "$1116.IPV6Traffic"
        },
        "IPV6Traffic|1117": {
            $sum: "$1117.IPV6Traffic"
        },
        "IPV6Traffic|1118": {
            $sum: "$1118.IPV6Traffic"
        },
        "IPV6Traffic|1119": {
            $sum: "$1119.IPV6Traffic"
        },
        "IPV6Traffic|1120": {
            $sum: "$1120.IPV6Traffic"
        },
        "IPV6Traffic|1121": {
            $sum: "$1121.IPV6Traffic"
        },
        "IPV6Traffic|1122": {
            $sum: "$1122.IPV6Traffic"
        },
        "IPV6Traffic|1123": {
            $sum: "$1123.IPV6Traffic"
        },
        "IPV6Traffic|1124": {
            $sum: "$1124.IPV6Traffic"
        },
        "IPV6Traffic|1125": {
            $sum: "$1125.IPV6Traffic"
        },
        "IPV6Traffic|1126": {
            $sum: "$1126.IPV6Traffic"
        },
        "IPV6Traffic|1127": {
            $sum: "$1127.IPV6Traffic"
        },
        "IPV6Traffic|1128": {
            $sum: "$1128.IPV6Traffic"
        },
        "IPV6Traffic|1129": {
            $sum: "$1129.IPV6Traffic"
        },
        "IPV6Traffic|1130": {
            $sum: "$1130.IPV6Traffic"
        },
        "IPV6Traffic|1131": {
            $sum: "$1131.IPV6Traffic"
        },
        "IPV6Traffic|1132": {
            $sum: "$1132.IPV6Traffic"
        },
        "IPV6Traffic|1133": {
            $sum: "$1133.IPV6Traffic"
        },
        "IPV6Traffic|1134": {
            $sum: "$1134.IPV6Traffic"
        },
        "IPV6Traffic|1135": {
            $sum: "$1135.IPV6Traffic"
        },
        "IPV6Traffic|1136": {
            $sum: "$1136.IPV6Traffic"
        },
        "IPV6Traffic|1137": {
            $sum: "$1137.IPV6Traffic"
        },
        "IPV6Traffic|1138": {
            $sum: "$1138.IPV6Traffic"
        },
        "IPV6Traffic|1139": {
            $sum: "$1139.IPV6Traffic"
        },
        "IPV6Traffic|1140": {
            $sum: "$1140.IPV6Traffic"
        },
        "IPV6Traffic|1141": {
            $sum: "$1141.IPV6Traffic"
        },
        "IPV6Traffic|1142": {
            $sum: "$1142.IPV6Traffic"
        },
        "IPV6Traffic|1143": {
            $sum: "$1143.IPV6Traffic"
        },
        "IPV6Traffic|1144": {
            $sum: "$1144.IPV6Traffic"
        },
        "IPV6Traffic|1145": {
            $sum: "$1145.IPV6Traffic"
        },
        "IPV6Traffic|1146": {
            $sum: "$1146.IPV6Traffic"
        },
        "IPV6Traffic|1147": {
            $sum: "$1147.IPV6Traffic"
        },
        "IPV6Traffic|1148": {
            $sum: "$1148.IPV6Traffic"
        },
        "IPV6Traffic|1149": {
            $sum: "$1149.IPV6Traffic"
        },
        "IPV6Traffic|1150": {
            $sum: "$1150.IPV6Traffic"
        },
        "IPV6Traffic|1151": {
            $sum: "$1151.IPV6Traffic"
        },
        "IPV6Traffic|1152": {
            $sum: "$1152.IPV6Traffic"
        },
        "IPV6Traffic|1153": {
            $sum: "$1153.IPV6Traffic"
        },
        "IPV6Traffic|1154": {
            $sum: "$1154.IPV6Traffic"
        },
        "IPV6Traffic|1155": {
            $sum: "$1155.IPV6Traffic"
        },
        "IPV6Traffic|1156": {
            $sum: "$1156.IPV6Traffic"
        },
        "IPV6Traffic|1157": {
            $sum: "$1157.IPV6Traffic"
        },
        "IPV6Traffic|1158": {
            $sum: "$1158.IPV6Traffic"
        },
        "IPV6Traffic|1159": {
            $sum: "$1159.IPV6Traffic"
        },
        "IPV6Traffic|1200": {
            $sum: "$1200.IPV6Traffic"
        },
        "IPV6Traffic|1201": {
            $sum: "$1201.IPV6Traffic"
        },
        "IPV6Traffic|1202": {
            $sum: "$1202.IPV6Traffic"
        },
        "IPV6Traffic|1203": {
            $sum: "$1203.IPV6Traffic"
        },
        "IPV6Traffic|1204": {
            $sum: "$1204.IPV6Traffic"
        },
        "IPV6Traffic|1205": {
            $sum: "$1205.IPV6Traffic"
        },
        "IPV6Traffic|1206": {
            $sum: "$1206.IPV6Traffic"
        },
        "IPV6Traffic|1207": {
            $sum: "$1207.IPV6Traffic"
        },
        "IPV6Traffic|1208": {
            $sum: "$1208.IPV6Traffic"
        },
        "IPV6Traffic|1209": {
            $sum: "$1209.IPV6Traffic"
        },
        "IPV6Traffic|1210": {
            $sum: "$1210.IPV6Traffic"
        },
        "IPV6Traffic|1211": {
            $sum: "$1211.IPV6Traffic"
        },
        "IPV6Traffic|1212": {
            $sum: "$1212.IPV6Traffic"
        },
        "IPV6Traffic|1213": {
            $sum: "$1213.IPV6Traffic"
        },
        "IPV6Traffic|1214": {
            $sum: "$1214.IPV6Traffic"
        },
        "IPV6Traffic|1215": {
            $sum: "$1215.IPV6Traffic"
        },
        "IPV6Traffic|1216": {
            $sum: "$1216.IPV6Traffic"
        },
        "IPV6Traffic|1217": {
            $sum: "$1217.IPV6Traffic"
        },
        "IPV6Traffic|1218": {
            $sum: "$1218.IPV6Traffic"
        },
        "IPV6Traffic|1219": {
            $sum: "$1219.IPV6Traffic"
        },
        "IPV6Traffic|1220": {
            $sum: "$1220.IPV6Traffic"
        },
        "IPV6Traffic|1221": {
            $sum: "$1221.IPV6Traffic"
        },
        "IPV6Traffic|1222": {
            $sum: "$1222.IPV6Traffic"
        },
        "IPV6Traffic|1223": {
            $sum: "$1223.IPV6Traffic"
        },
        "IPV6Traffic|1224": {
            $sum: "$1224.IPV6Traffic"
        },
        "IPV6Traffic|1225": {
            $sum: "$1225.IPV6Traffic"
        },
        "IPV6Traffic|1226": {
            $sum: "$1226.IPV6Traffic"
        },
        "IPV6Traffic|1227": {
            $sum: "$1227.IPV6Traffic"
        },
        "IPV6Traffic|1228": {
            $sum: "$1228.IPV6Traffic"
        },
        "IPV6Traffic|1229": {
            $sum: "$1229.IPV6Traffic"
        },
        "IPV6Traffic|1230": {
            $sum: "$1230.IPV6Traffic"
        },
        "IPV6Traffic|1231": {
            $sum: "$1231.IPV6Traffic"
        },
        "IPV6Traffic|1232": {
            $sum: "$1232.IPV6Traffic"
        },
        "IPV6Traffic|1233": {
            $sum: "$1233.IPV6Traffic"
        },
        "IPV6Traffic|1234": {
            $sum: "$1234.IPV6Traffic"
        },
        "IPV6Traffic|1235": {
            $sum: "$1235.IPV6Traffic"
        },
        "IPV6Traffic|1236": {
            $sum: "$1236.IPV6Traffic"
        },
        "IPV6Traffic|1237": {
            $sum: "$1237.IPV6Traffic"
        },
        "IPV6Traffic|1238": {
            $sum: "$1238.IPV6Traffic"
        },
        "IPV6Traffic|1239": {
            $sum: "$1239.IPV6Traffic"
        },
        "IPV6Traffic|1240": {
            $sum: "$1240.IPV6Traffic"
        },
        "IPV6Traffic|1241": {
            $sum: "$1241.IPV6Traffic"
        },
        "IPV6Traffic|1242": {
            $sum: "$1242.IPV6Traffic"
        },
        "IPV6Traffic|1243": {
            $sum: "$1243.IPV6Traffic"
        },
        "IPV6Traffic|1244": {
            $sum: "$1244.IPV6Traffic"
        },
        "IPV6Traffic|1245": {
            $sum: "$1245.IPV6Traffic"
        },
        "IPV6Traffic|1246": {
            $sum: "$1246.IPV6Traffic"
        },
        "IPV6Traffic|1247": {
            $sum: "$1247.IPV6Traffic"
        },
        "IPV6Traffic|1248": {
            $sum: "$1248.IPV6Traffic"
        },
        "IPV6Traffic|1249": {
            $sum: "$1249.IPV6Traffic"
        },
        "IPV6Traffic|1250": {
            $sum: "$1250.IPV6Traffic"
        },
        "IPV6Traffic|1251": {
            $sum: "$1251.IPV6Traffic"
        },
        "IPV6Traffic|1252": {
            $sum: "$1252.IPV6Traffic"
        },
        "IPV6Traffic|1253": {
            $sum: "$1253.IPV6Traffic"
        },
        "IPV6Traffic|1254": {
            $sum: "$1254.IPV6Traffic"
        },
        "IPV6Traffic|1255": {
            $sum: "$1255.IPV6Traffic"
        },
        "IPV6Traffic|1256": {
            $sum: "$1256.IPV6Traffic"
        },
        "IPV6Traffic|1257": {
            $sum: "$1257.IPV6Traffic"
        },
        "IPV6Traffic|1258": {
            $sum: "$1258.IPV6Traffic"
        },
        "IPV6Traffic|1259": {
            $sum: "$1259.IPV6Traffic"
        },
        "IPV6Traffic|1300": {
            $sum: "$1300.IPV6Traffic"
        },
        "IPV6Traffic|1301": {
            $sum: "$1301.IPV6Traffic"
        },
        "IPV6Traffic|1302": {
            $sum: "$1302.IPV6Traffic"
        },
        "IPV6Traffic|1303": {
            $sum: "$1303.IPV6Traffic"
        },
        "IPV6Traffic|1304": {
            $sum: "$1304.IPV6Traffic"
        },
        "IPV6Traffic|1305": {
            $sum: "$1305.IPV6Traffic"
        },
        "IPV6Traffic|1306": {
            $sum: "$1306.IPV6Traffic"
        },
        "IPV6Traffic|1307": {
            $sum: "$1307.IPV6Traffic"
        },
        "IPV6Traffic|1308": {
            $sum: "$1308.IPV6Traffic"
        },
        "IPV6Traffic|1309": {
            $sum: "$1309.IPV6Traffic"
        },
        "IPV6Traffic|1310": {
            $sum: "$1310.IPV6Traffic"
        },
        "IPV6Traffic|1311": {
            $sum: "$1311.IPV6Traffic"
        },
        "IPV6Traffic|1312": {
            $sum: "$1312.IPV6Traffic"
        },
        "IPV6Traffic|1313": {
            $sum: "$1313.IPV6Traffic"
        },
        "IPV6Traffic|1314": {
            $sum: "$1314.IPV6Traffic"
        },
        "IPV6Traffic|1315": {
            $sum: "$1315.IPV6Traffic"
        },
        "IPV6Traffic|1316": {
            $sum: "$1316.IPV6Traffic"
        },
        "IPV6Traffic|1317": {
            $sum: "$1317.IPV6Traffic"
        },
        "IPV6Traffic|1318": {
            $sum: "$1318.IPV6Traffic"
        },
        "IPV6Traffic|1319": {
            $sum: "$1319.IPV6Traffic"
        },
        "IPV6Traffic|1320": {
            $sum: "$1320.IPV6Traffic"
        },
        "IPV6Traffic|1321": {
            $sum: "$1321.IPV6Traffic"
        },
        "IPV6Traffic|1322": {
            $sum: "$1322.IPV6Traffic"
        },
        "IPV6Traffic|1323": {
            $sum: "$1323.IPV6Traffic"
        },
        "IPV6Traffic|1324": {
            $sum: "$1324.IPV6Traffic"
        },
        "IPV6Traffic|1325": {
            $sum: "$1325.IPV6Traffic"
        },
        "IPV6Traffic|1326": {
            $sum: "$1326.IPV6Traffic"
        },
        "IPV6Traffic|1327": {
            $sum: "$1327.IPV6Traffic"
        },
        "IPV6Traffic|1328": {
            $sum: "$1328.IPV6Traffic"
        },
        "IPV6Traffic|1329": {
            $sum: "$1329.IPV6Traffic"
        },
        "IPV6Traffic|1330": {
            $sum: "$1330.IPV6Traffic"
        },
        "IPV6Traffic|1331": {
            $sum: "$1331.IPV6Traffic"
        },
        "IPV6Traffic|1332": {
            $sum: "$1332.IPV6Traffic"
        },
        "IPV6Traffic|1333": {
            $sum: "$1333.IPV6Traffic"
        },
        "IPV6Traffic|1334": {
            $sum: "$1334.IPV6Traffic"
        },
        "IPV6Traffic|1335": {
            $sum: "$1335.IPV6Traffic"
        },
        "IPV6Traffic|1336": {
            $sum: "$1336.IPV6Traffic"
        },
        "IPV6Traffic|1337": {
            $sum: "$1337.IPV6Traffic"
        },
        "IPV6Traffic|1338": {
            $sum: "$1338.IPV6Traffic"
        },
        "IPV6Traffic|1339": {
            $sum: "$1339.IPV6Traffic"
        },
        "IPV6Traffic|1340": {
            $sum: "$1340.IPV6Traffic"
        },
        "IPV6Traffic|1341": {
            $sum: "$1341.IPV6Traffic"
        },
        "IPV6Traffic|1342": {
            $sum: "$1342.IPV6Traffic"
        },
        "IPV6Traffic|1343": {
            $sum: "$1343.IPV6Traffic"
        },
        "IPV6Traffic|1344": {
            $sum: "$1344.IPV6Traffic"
        },
        "IPV6Traffic|1345": {
            $sum: "$1345.IPV6Traffic"
        },
        "IPV6Traffic|1346": {
            $sum: "$1346.IPV6Traffic"
        },
        "IPV6Traffic|1347": {
            $sum: "$1347.IPV6Traffic"
        },
        "IPV6Traffic|1348": {
            $sum: "$1348.IPV6Traffic"
        },
        "IPV6Traffic|1349": {
            $sum: "$1349.IPV6Traffic"
        },
        "IPV6Traffic|1350": {
            $sum: "$1350.IPV6Traffic"
        },
        "IPV6Traffic|1351": {
            $sum: "$1351.IPV6Traffic"
        },
        "IPV6Traffic|1352": {
            $sum: "$1352.IPV6Traffic"
        },
        "IPV6Traffic|1353": {
            $sum: "$1353.IPV6Traffic"
        },
        "IPV6Traffic|1354": {
            $sum: "$1354.IPV6Traffic"
        },
        "IPV6Traffic|1355": {
            $sum: "$1355.IPV6Traffic"
        },
        "IPV6Traffic|1356": {
            $sum: "$1356.IPV6Traffic"
        },
        "IPV6Traffic|1357": {
            $sum: "$1357.IPV6Traffic"
        },
        "IPV6Traffic|1358": {
            $sum: "$1358.IPV6Traffic"
        },
        "IPV6Traffic|1359": {
            $sum: "$1359.IPV6Traffic"
        },
        "IPV6Traffic|1400": {
            $sum: "$1400.IPV6Traffic"
        },
        "IPV6Traffic|1401": {
            $sum: "$1401.IPV6Traffic"
        },
        "IPV6Traffic|1402": {
            $sum: "$1402.IPV6Traffic"
        },
        "IPV6Traffic|1403": {
            $sum: "$1403.IPV6Traffic"
        },
        "IPV6Traffic|1404": {
            $sum: "$1404.IPV6Traffic"
        },
        "IPV6Traffic|1405": {
            $sum: "$1405.IPV6Traffic"
        },
        "IPV6Traffic|1406": {
            $sum: "$1406.IPV6Traffic"
        },
        "IPV6Traffic|1407": {
            $sum: "$1407.IPV6Traffic"
        },
        "IPV6Traffic|1408": {
            $sum: "$1408.IPV6Traffic"
        },
        "IPV6Traffic|1409": {
            $sum: "$1409.IPV6Traffic"
        },
        "IPV6Traffic|1410": {
            $sum: "$1410.IPV6Traffic"
        },
        "IPV6Traffic|1411": {
            $sum: "$1411.IPV6Traffic"
        },
        "IPV6Traffic|1412": {
            $sum: "$1412.IPV6Traffic"
        },
        "IPV6Traffic|1413": {
            $sum: "$1413.IPV6Traffic"
        },
        "IPV6Traffic|1414": {
            $sum: "$1414.IPV6Traffic"
        },
        "IPV6Traffic|1415": {
            $sum: "$1415.IPV6Traffic"
        },
        "IPV6Traffic|1416": {
            $sum: "$1416.IPV6Traffic"
        },
        "IPV6Traffic|1417": {
            $sum: "$1417.IPV6Traffic"
        },
        "IPV6Traffic|1418": {
            $sum: "$1418.IPV6Traffic"
        },
        "IPV6Traffic|1419": {
            $sum: "$1419.IPV6Traffic"
        },
        "IPV6Traffic|1420": {
            $sum: "$1420.IPV6Traffic"
        },
        "IPV6Traffic|1421": {
            $sum: "$1421.IPV6Traffic"
        },
        "IPV6Traffic|1422": {
            $sum: "$1422.IPV6Traffic"
        },
        "IPV6Traffic|1423": {
            $sum: "$1423.IPV6Traffic"
        },
        "IPV6Traffic|1424": {
            $sum: "$1424.IPV6Traffic"
        },
        "IPV6Traffic|1425": {
            $sum: "$1425.IPV6Traffic"
        },
        "IPV6Traffic|1426": {
            $sum: "$1426.IPV6Traffic"
        },
        "IPV6Traffic|1427": {
            $sum: "$1427.IPV6Traffic"
        },
        "IPV6Traffic|1428": {
            $sum: "$1428.IPV6Traffic"
        },
        "IPV6Traffic|1429": {
            $sum: "$1429.IPV6Traffic"
        },
        "IPV6Traffic|1430": {
            $sum: "$1430.IPV6Traffic"
        },
        "IPV6Traffic|1431": {
            $sum: "$1431.IPV6Traffic"
        },
        "IPV6Traffic|1432": {
            $sum: "$1432.IPV6Traffic"
        },
        "IPV6Traffic|1433": {
            $sum: "$1433.IPV6Traffic"
        },
        "IPV6Traffic|1434": {
            $sum: "$1434.IPV6Traffic"
        },
        "IPV6Traffic|1435": {
            $sum: "$1435.IPV6Traffic"
        },
        "IPV6Traffic|1436": {
            $sum: "$1436.IPV6Traffic"
        },
        "IPV6Traffic|1437": {
            $sum: "$1437.IPV6Traffic"
        },
        "IPV6Traffic|1438": {
            $sum: "$1438.IPV6Traffic"
        },
        "IPV6Traffic|1439": {
            $sum: "$1439.IPV6Traffic"
        },
        "IPV6Traffic|1440": {
            $sum: "$1440.IPV6Traffic"
        },
        "IPV6Traffic|1441": {
            $sum: "$1441.IPV6Traffic"
        },
        "IPV6Traffic|1442": {
            $sum: "$1442.IPV6Traffic"
        },
        "IPV6Traffic|1443": {
            $sum: "$1443.IPV6Traffic"
        },
        "IPV6Traffic|1444": {
            $sum: "$1444.IPV6Traffic"
        },
        "IPV6Traffic|1445": {
            $sum: "$1445.IPV6Traffic"
        },
        "IPV6Traffic|1446": {
            $sum: "$1446.IPV6Traffic"
        },
        "IPV6Traffic|1447": {
            $sum: "$1447.IPV6Traffic"
        },
        "IPV6Traffic|1448": {
            $sum: "$1448.IPV6Traffic"
        },
        "IPV6Traffic|1449": {
            $sum: "$1449.IPV6Traffic"
        },
        "IPV6Traffic|1450": {
            $sum: "$1450.IPV6Traffic"
        },
        "IPV6Traffic|1451": {
            $sum: "$1451.IPV6Traffic"
        },
        "IPV6Traffic|1452": {
            $sum: "$1452.IPV6Traffic"
        },
        "IPV6Traffic|1453": {
            $sum: "$1453.IPV6Traffic"
        },
        "IPV6Traffic|1454": {
            $sum: "$1454.IPV6Traffic"
        },
        "IPV6Traffic|1455": {
            $sum: "$1455.IPV6Traffic"
        },
        "IPV6Traffic|1456": {
            $sum: "$1456.IPV6Traffic"
        },
        "IPV6Traffic|1457": {
            $sum: "$1457.IPV6Traffic"
        },
        "IPV6Traffic|1458": {
            $sum: "$1458.IPV6Traffic"
        },
        "IPV6Traffic|1459": {
            $sum: "$1459.IPV6Traffic"
        },
        "IPV6Traffic|1500": {
            $sum: "$1500.IPV6Traffic"
        },
        "IPV6Traffic|1501": {
            $sum: "$1501.IPV6Traffic"
        },
        "IPV6Traffic|1502": {
            $sum: "$1502.IPV6Traffic"
        },
        "IPV6Traffic|1503": {
            $sum: "$1503.IPV6Traffic"
        },
        "IPV6Traffic|1504": {
            $sum: "$1504.IPV6Traffic"
        },
        "IPV6Traffic|1505": {
            $sum: "$1505.IPV6Traffic"
        },
        "IPV6Traffic|1506": {
            $sum: "$1506.IPV6Traffic"
        },
        "IPV6Traffic|1507": {
            $sum: "$1507.IPV6Traffic"
        },
        "IPV6Traffic|1508": {
            $sum: "$1508.IPV6Traffic"
        },
        "IPV6Traffic|1509": {
            $sum: "$1509.IPV6Traffic"
        },
        "IPV6Traffic|1510": {
            $sum: "$1510.IPV6Traffic"
        },
        "IPV6Traffic|1511": {
            $sum: "$1511.IPV6Traffic"
        },
        "IPV6Traffic|1512": {
            $sum: "$1512.IPV6Traffic"
        },
        "IPV6Traffic|1513": {
            $sum: "$1513.IPV6Traffic"
        },
        "IPV6Traffic|1514": {
            $sum: "$1514.IPV6Traffic"
        },
        "IPV6Traffic|1515": {
            $sum: "$1515.IPV6Traffic"
        },
        "IPV6Traffic|1516": {
            $sum: "$1516.IPV6Traffic"
        },
        "IPV6Traffic|1517": {
            $sum: "$1517.IPV6Traffic"
        },
        "IPV6Traffic|1518": {
            $sum: "$1518.IPV6Traffic"
        },
        "IPV6Traffic|1519": {
            $sum: "$1519.IPV6Traffic"
        },
        "IPV6Traffic|1520": {
            $sum: "$1520.IPV6Traffic"
        },
        "IPV6Traffic|1521": {
            $sum: "$1521.IPV6Traffic"
        },
        "IPV6Traffic|1522": {
            $sum: "$1522.IPV6Traffic"
        },
        "IPV6Traffic|1523": {
            $sum: "$1523.IPV6Traffic"
        },
        "IPV6Traffic|1524": {
            $sum: "$1524.IPV6Traffic"
        },
        "IPV6Traffic|1525": {
            $sum: "$1525.IPV6Traffic"
        },
        "IPV6Traffic|1526": {
            $sum: "$1526.IPV6Traffic"
        },
        "IPV6Traffic|1527": {
            $sum: "$1527.IPV6Traffic"
        },
        "IPV6Traffic|1528": {
            $sum: "$1528.IPV6Traffic"
        },
        "IPV6Traffic|1529": {
            $sum: "$1529.IPV6Traffic"
        },
        "IPV6Traffic|1530": {
            $sum: "$1530.IPV6Traffic"
        },
        "IPV6Traffic|1531": {
            $sum: "$1531.IPV6Traffic"
        },
        "IPV6Traffic|1532": {
            $sum: "$1532.IPV6Traffic"
        },
        "IPV6Traffic|1533": {
            $sum: "$1533.IPV6Traffic"
        },
        "IPV6Traffic|1534": {
            $sum: "$1534.IPV6Traffic"
        },
        "IPV6Traffic|1535": {
            $sum: "$1535.IPV6Traffic"
        },
        "IPV6Traffic|1536": {
            $sum: "$1536.IPV6Traffic"
        },
        "IPV6Traffic|1537": {
            $sum: "$1537.IPV6Traffic"
        },
        "IPV6Traffic|1538": {
            $sum: "$1538.IPV6Traffic"
        },
        "IPV6Traffic|1539": {
            $sum: "$1539.IPV6Traffic"
        },
        "IPV6Traffic|1540": {
            $sum: "$1540.IPV6Traffic"
        },
        "IPV6Traffic|1541": {
            $sum: "$1541.IPV6Traffic"
        },
        "IPV6Traffic|1542": {
            $sum: "$1542.IPV6Traffic"
        },
        "IPV6Traffic|1543": {
            $sum: "$1543.IPV6Traffic"
        },
        "IPV6Traffic|1544": {
            $sum: "$1544.IPV6Traffic"
        },
        "IPV6Traffic|1545": {
            $sum: "$1545.IPV6Traffic"
        },
        "IPV6Traffic|1546": {
            $sum: "$1546.IPV6Traffic"
        },
        "IPV6Traffic|1547": {
            $sum: "$1547.IPV6Traffic"
        },
        "IPV6Traffic|1548": {
            $sum: "$1548.IPV6Traffic"
        },
        "IPV6Traffic|1549": {
            $sum: "$1549.IPV6Traffic"
        },
        "IPV6Traffic|1550": {
            $sum: "$1550.IPV6Traffic"
        },
        "IPV6Traffic|1551": {
            $sum: "$1551.IPV6Traffic"
        },
        "IPV6Traffic|1552": {
            $sum: "$1552.IPV6Traffic"
        },
        "IPV6Traffic|1553": {
            $sum: "$1553.IPV6Traffic"
        },
        "IPV6Traffic|1554": {
            $sum: "$1554.IPV6Traffic"
        },
        "IPV6Traffic|1555": {
            $sum: "$1555.IPV6Traffic"
        },
        "IPV6Traffic|1556": {
            $sum: "$1556.IPV6Traffic"
        },
        "IPV6Traffic|1557": {
            $sum: "$1557.IPV6Traffic"
        },
        "IPV6Traffic|1558": {
            $sum: "$1558.IPV6Traffic"
        },
        "IPV6Traffic|1559": {
            $sum: "$1559.IPV6Traffic"
        },
        "IPV6Traffic|1600": {
            $sum: "$1600.IPV6Traffic"
        },
        "IPV6Traffic|1601": {
            $sum: "$1601.IPV6Traffic"
        },
        "IPV6Traffic|1602": {
            $sum: "$1602.IPV6Traffic"
        },
        "IPV6Traffic|1603": {
            $sum: "$1603.IPV6Traffic"
        },
        "IPV6Traffic|1604": {
            $sum: "$1604.IPV6Traffic"
        },
        "IPV6Traffic|1605": {
            $sum: "$1605.IPV6Traffic"
        },
        "IPV6Traffic|1606": {
            $sum: "$1606.IPV6Traffic"
        },
        "IPV6Traffic|1607": {
            $sum: "$1607.IPV6Traffic"
        },
        "IPV6Traffic|1608": {
            $sum: "$1608.IPV6Traffic"
        },
        "IPV6Traffic|1609": {
            $sum: "$1609.IPV6Traffic"
        },
        "IPV6Traffic|1610": {
            $sum: "$1610.IPV6Traffic"
        },
        "IPV6Traffic|1611": {
            $sum: "$1611.IPV6Traffic"
        },
        "IPV6Traffic|1612": {
            $sum: "$1612.IPV6Traffic"
        },
        "IPV6Traffic|1613": {
            $sum: "$1613.IPV6Traffic"
        },
        "IPV6Traffic|1614": {
            $sum: "$1614.IPV6Traffic"
        },
        "IPV6Traffic|1615": {
            $sum: "$1615.IPV6Traffic"
        },
        "IPV6Traffic|1616": {
            $sum: "$1616.IPV6Traffic"
        },
        "IPV6Traffic|1617": {
            $sum: "$1617.IPV6Traffic"
        },
        "IPV6Traffic|1618": {
            $sum: "$1618.IPV6Traffic"
        },
        "IPV6Traffic|1619": {
            $sum: "$1619.IPV6Traffic"
        },
        "IPV6Traffic|1620": {
            $sum: "$1620.IPV6Traffic"
        },
        "IPV6Traffic|1621": {
            $sum: "$1621.IPV6Traffic"
        },
        "IPV6Traffic|1622": {
            $sum: "$1622.IPV6Traffic"
        },
        "IPV6Traffic|1623": {
            $sum: "$1623.IPV6Traffic"
        },
        "IPV6Traffic|1624": {
            $sum: "$1624.IPV6Traffic"
        },
        "IPV6Traffic|1625": {
            $sum: "$1625.IPV6Traffic"
        },
        "IPV6Traffic|1626": {
            $sum: "$1626.IPV6Traffic"
        },
        "IPV6Traffic|1627": {
            $sum: "$1627.IPV6Traffic"
        },
        "IPV6Traffic|1628": {
            $sum: "$1628.IPV6Traffic"
        },
        "IPV6Traffic|1629": {
            $sum: "$1629.IPV6Traffic"
        },
        "IPV6Traffic|1630": {
            $sum: "$1630.IPV6Traffic"
        },
        "IPV6Traffic|1631": {
            $sum: "$1631.IPV6Traffic"
        },
        "IPV6Traffic|1632": {
            $sum: "$1632.IPV6Traffic"
        },
        "IPV6Traffic|1633": {
            $sum: "$1633.IPV6Traffic"
        },
        "IPV6Traffic|1634": {
            $sum: "$1634.IPV6Traffic"
        },
        "IPV6Traffic|1635": {
            $sum: "$1635.IPV6Traffic"
        },
        "IPV6Traffic|1636": {
            $sum: "$1636.IPV6Traffic"
        },
        "IPV6Traffic|1637": {
            $sum: "$1637.IPV6Traffic"
        },
        "IPV6Traffic|1638": {
            $sum: "$1638.IPV6Traffic"
        },
        "IPV6Traffic|1639": {
            $sum: "$1639.IPV6Traffic"
        },
        "IPV6Traffic|1640": {
            $sum: "$1640.IPV6Traffic"
        },
        "IPV6Traffic|1641": {
            $sum: "$1641.IPV6Traffic"
        },
        "IPV6Traffic|1642": {
            $sum: "$1642.IPV6Traffic"
        },
        "IPV6Traffic|1643": {
            $sum: "$1643.IPV6Traffic"
        },
        "IPV6Traffic|1644": {
            $sum: "$1644.IPV6Traffic"
        },
        "IPV6Traffic|1645": {
            $sum: "$1645.IPV6Traffic"
        },
        "IPV6Traffic|1646": {
            $sum: "$1646.IPV6Traffic"
        },
        "IPV6Traffic|1647": {
            $sum: "$1647.IPV6Traffic"
        },
        "IPV6Traffic|1648": {
            $sum: "$1648.IPV6Traffic"
        },
        "IPV6Traffic|1649": {
            $sum: "$1649.IPV6Traffic"
        },
        "IPV6Traffic|1650": {
            $sum: "$1650.IPV6Traffic"
        },
        "IPV6Traffic|1651": {
            $sum: "$1651.IPV6Traffic"
        },
        "IPV6Traffic|1652": {
            $sum: "$1652.IPV6Traffic"
        },
        "IPV6Traffic|1653": {
            $sum: "$1653.IPV6Traffic"
        },
        "IPV6Traffic|1654": {
            $sum: "$1654.IPV6Traffic"
        },
        "IPV6Traffic|1655": {
            $sum: "$1655.IPV6Traffic"
        },
        "IPV6Traffic|1656": {
            $sum: "$1656.IPV6Traffic"
        },
        "IPV6Traffic|1657": {
            $sum: "$1657.IPV6Traffic"
        },
        "IPV6Traffic|1658": {
            $sum: "$1658.IPV6Traffic"
        },
        "IPV6Traffic|1659": {
            $sum: "$1659.IPV6Traffic"
        },
        "IPV6Traffic|1700": {
            $sum: "$1700.IPV6Traffic"
        },
        "IPV6Traffic|1701": {
            $sum: "$1701.IPV6Traffic"
        },
        "IPV6Traffic|1702": {
            $sum: "$1702.IPV6Traffic"
        },
        "IPV6Traffic|1703": {
            $sum: "$1703.IPV6Traffic"
        },
        "IPV6Traffic|1704": {
            $sum: "$1704.IPV6Traffic"
        },
        "IPV6Traffic|1705": {
            $sum: "$1705.IPV6Traffic"
        },
        "IPV6Traffic|1706": {
            $sum: "$1706.IPV6Traffic"
        },
        "IPV6Traffic|1707": {
            $sum: "$1707.IPV6Traffic"
        },
        "IPV6Traffic|1708": {
            $sum: "$1708.IPV6Traffic"
        },
        "IPV6Traffic|1709": {
            $sum: "$1709.IPV6Traffic"
        },
        "IPV6Traffic|1710": {
            $sum: "$1710.IPV6Traffic"
        },
        "IPV6Traffic|1711": {
            $sum: "$1711.IPV6Traffic"
        },
        "IPV6Traffic|1712": {
            $sum: "$1712.IPV6Traffic"
        },
        "IPV6Traffic|1713": {
            $sum: "$1713.IPV6Traffic"
        },
        "IPV6Traffic|1714": {
            $sum: "$1714.IPV6Traffic"
        },
        "IPV6Traffic|1715": {
            $sum: "$1715.IPV6Traffic"
        },
        "IPV6Traffic|1716": {
            $sum: "$1716.IPV6Traffic"
        },
        "IPV6Traffic|1717": {
            $sum: "$1717.IPV6Traffic"
        },
        "IPV6Traffic|1718": {
            $sum: "$1718.IPV6Traffic"
        },
        "IPV6Traffic|1719": {
            $sum: "$1719.IPV6Traffic"
        },
        "IPV6Traffic|1720": {
            $sum: "$1720.IPV6Traffic"
        },
        "IPV6Traffic|1721": {
            $sum: "$1721.IPV6Traffic"
        },
        "IPV6Traffic|1722": {
            $sum: "$1722.IPV6Traffic"
        },
        "IPV6Traffic|1723": {
            $sum: "$1723.IPV6Traffic"
        },
        "IPV6Traffic|1724": {
            $sum: "$1724.IPV6Traffic"
        },
        "IPV6Traffic|1725": {
            $sum: "$1725.IPV6Traffic"
        },
        "IPV6Traffic|1726": {
            $sum: "$1726.IPV6Traffic"
        },
        "IPV6Traffic|1727": {
            $sum: "$1727.IPV6Traffic"
        },
        "IPV6Traffic|1728": {
            $sum: "$1728.IPV6Traffic"
        },
        "IPV6Traffic|1729": {
            $sum: "$1729.IPV6Traffic"
        },
        "IPV6Traffic|1730": {
            $sum: "$1730.IPV6Traffic"
        },
        "IPV6Traffic|1731": {
            $sum: "$1731.IPV6Traffic"
        },
        "IPV6Traffic|1732": {
            $sum: "$1732.IPV6Traffic"
        },
        "IPV6Traffic|1733": {
            $sum: "$1733.IPV6Traffic"
        },
        "IPV6Traffic|1734": {
            $sum: "$1734.IPV6Traffic"
        },
        "IPV6Traffic|1735": {
            $sum: "$1735.IPV6Traffic"
        },
        "IPV6Traffic|1736": {
            $sum: "$1736.IPV6Traffic"
        },
        "IPV6Traffic|1737": {
            $sum: "$1737.IPV6Traffic"
        },
        "IPV6Traffic|1738": {
            $sum: "$1738.IPV6Traffic"
        },
        "IPV6Traffic|1739": {
            $sum: "$1739.IPV6Traffic"
        },
        "IPV6Traffic|1740": {
            $sum: "$1740.IPV6Traffic"
        },
        "IPV6Traffic|1741": {
            $sum: "$1741.IPV6Traffic"
        },
        "IPV6Traffic|1742": {
            $sum: "$1742.IPV6Traffic"
        },
        "IPV6Traffic|1743": {
            $sum: "$1743.IPV6Traffic"
        },
        "IPV6Traffic|1744": {
            $sum: "$1744.IPV6Traffic"
        },
        "IPV6Traffic|1745": {
            $sum: "$1745.IPV6Traffic"
        },
        "IPV6Traffic|1746": {
            $sum: "$1746.IPV6Traffic"
        },
        "IPV6Traffic|1747": {
            $sum: "$1747.IPV6Traffic"
        },
        "IPV6Traffic|1748": {
            $sum: "$1748.IPV6Traffic"
        },
        "IPV6Traffic|1749": {
            $sum: "$1749.IPV6Traffic"
        },
        "IPV6Traffic|1750": {
            $sum: "$1750.IPV6Traffic"
        },
        "IPV6Traffic|1751": {
            $sum: "$1751.IPV6Traffic"
        },
        "IPV6Traffic|1752": {
            $sum: "$1752.IPV6Traffic"
        },
        "IPV6Traffic|1753": {
            $sum: "$1753.IPV6Traffic"
        },
        "IPV6Traffic|1754": {
            $sum: "$1754.IPV6Traffic"
        },
        "IPV6Traffic|1755": {
            $sum: "$1755.IPV6Traffic"
        },
        "IPV6Traffic|1756": {
            $sum: "$1756.IPV6Traffic"
        },
        "IPV6Traffic|1757": {
            $sum: "$1757.IPV6Traffic"
        },
        "IPV6Traffic|1758": {
            $sum: "$1758.IPV6Traffic"
        },
        "IPV6Traffic|1759": {
            $sum: "$1759.IPV6Traffic"
        },
        "IPV6Traffic|1800": {
            $sum: "$1800.IPV6Traffic"
        },
        "IPV6Traffic|1801": {
            $sum: "$1801.IPV6Traffic"
        },
        "IPV6Traffic|1802": {
            $sum: "$1802.IPV6Traffic"
        },
        "IPV6Traffic|1803": {
            $sum: "$1803.IPV6Traffic"
        },
        "IPV6Traffic|1804": {
            $sum: "$1804.IPV6Traffic"
        },
        "IPV6Traffic|1805": {
            $sum: "$1805.IPV6Traffic"
        },
        "IPV6Traffic|1806": {
            $sum: "$1806.IPV6Traffic"
        },
        "IPV6Traffic|1807": {
            $sum: "$1807.IPV6Traffic"
        },
        "IPV6Traffic|1808": {
            $sum: "$1808.IPV6Traffic"
        },
        "IPV6Traffic|1809": {
            $sum: "$1809.IPV6Traffic"
        },
        "IPV6Traffic|1810": {
            $sum: "$1810.IPV6Traffic"
        },
        "IPV6Traffic|1811": {
            $sum: "$1811.IPV6Traffic"
        },
        "IPV6Traffic|1812": {
            $sum: "$1812.IPV6Traffic"
        },
        "IPV6Traffic|1813": {
            $sum: "$1813.IPV6Traffic"
        },
        "IPV6Traffic|1814": {
            $sum: "$1814.IPV6Traffic"
        },
        "IPV6Traffic|1815": {
            $sum: "$1815.IPV6Traffic"
        },
        "IPV6Traffic|1816": {
            $sum: "$1816.IPV6Traffic"
        },
        "IPV6Traffic|1817": {
            $sum: "$1817.IPV6Traffic"
        },
        "IPV6Traffic|1818": {
            $sum: "$1818.IPV6Traffic"
        },
        "IPV6Traffic|1819": {
            $sum: "$1819.IPV6Traffic"
        },
        "IPV6Traffic|1820": {
            $sum: "$1820.IPV6Traffic"
        },
        "IPV6Traffic|1821": {
            $sum: "$1821.IPV6Traffic"
        },
        "IPV6Traffic|1822": {
            $sum: "$1822.IPV6Traffic"
        },
        "IPV6Traffic|1823": {
            $sum: "$1823.IPV6Traffic"
        },
        "IPV6Traffic|1824": {
            $sum: "$1824.IPV6Traffic"
        },
        "IPV6Traffic|1825": {
            $sum: "$1825.IPV6Traffic"
        },
        "IPV6Traffic|1826": {
            $sum: "$1826.IPV6Traffic"
        },
        "IPV6Traffic|1827": {
            $sum: "$1827.IPV6Traffic"
        },
        "IPV6Traffic|1828": {
            $sum: "$1828.IPV6Traffic"
        },
        "IPV6Traffic|1829": {
            $sum: "$1829.IPV6Traffic"
        },
        "IPV6Traffic|1830": {
            $sum: "$1830.IPV6Traffic"
        },
        "IPV6Traffic|1831": {
            $sum: "$1831.IPV6Traffic"
        },
        "IPV6Traffic|1832": {
            $sum: "$1832.IPV6Traffic"
        },
        "IPV6Traffic|1833": {
            $sum: "$1833.IPV6Traffic"
        },
        "IPV6Traffic|1834": {
            $sum: "$1834.IPV6Traffic"
        },
        "IPV6Traffic|1835": {
            $sum: "$1835.IPV6Traffic"
        },
        "IPV6Traffic|1836": {
            $sum: "$1836.IPV6Traffic"
        },
        "IPV6Traffic|1837": {
            $sum: "$1837.IPV6Traffic"
        },
        "IPV6Traffic|1838": {
            $sum: "$1838.IPV6Traffic"
        },
        "IPV6Traffic|1839": {
            $sum: "$1839.IPV6Traffic"
        },
        "IPV6Traffic|1840": {
            $sum: "$1840.IPV6Traffic"
        },
        "IPV6Traffic|1841": {
            $sum: "$1841.IPV6Traffic"
        },
        "IPV6Traffic|1842": {
            $sum: "$1842.IPV6Traffic"
        },
        "IPV6Traffic|1843": {
            $sum: "$1843.IPV6Traffic"
        },
        "IPV6Traffic|1844": {
            $sum: "$1844.IPV6Traffic"
        },
        "IPV6Traffic|1845": {
            $sum: "$1845.IPV6Traffic"
        },
        "IPV6Traffic|1846": {
            $sum: "$1846.IPV6Traffic"
        },
        "IPV6Traffic|1847": {
            $sum: "$1847.IPV6Traffic"
        },
        "IPV6Traffic|1848": {
            $sum: "$1848.IPV6Traffic"
        },
        "IPV6Traffic|1849": {
            $sum: "$1849.IPV6Traffic"
        },
        "IPV6Traffic|1850": {
            $sum: "$1850.IPV6Traffic"
        },
        "IPV6Traffic|1851": {
            $sum: "$1851.IPV6Traffic"
        },
        "IPV6Traffic|1852": {
            $sum: "$1852.IPV6Traffic"
        },
        "IPV6Traffic|1853": {
            $sum: "$1853.IPV6Traffic"
        },
        "IPV6Traffic|1854": {
            $sum: "$1854.IPV6Traffic"
        },
        "IPV6Traffic|1855": {
            $sum: "$1855.IPV6Traffic"
        },
        "IPV6Traffic|1856": {
            $sum: "$1856.IPV6Traffic"
        },
        "IPV6Traffic|1857": {
            $sum: "$1857.IPV6Traffic"
        },
        "IPV6Traffic|1858": {
            $sum: "$1858.IPV6Traffic"
        },
        "IPV6Traffic|1859": {
            $sum: "$1859.IPV6Traffic"
        },
        "IPV6Traffic|1900": {
            $sum: "$1900.IPV6Traffic"
        },
        "IPV6Traffic|1901": {
            $sum: "$1901.IPV6Traffic"
        },
        "IPV6Traffic|1902": {
            $sum: "$1902.IPV6Traffic"
        },
        "IPV6Traffic|1903": {
            $sum: "$1903.IPV6Traffic"
        },
        "IPV6Traffic|1904": {
            $sum: "$1904.IPV6Traffic"
        },
        "IPV6Traffic|1905": {
            $sum: "$1905.IPV6Traffic"
        },
        "IPV6Traffic|1906": {
            $sum: "$1906.IPV6Traffic"
        },
        "IPV6Traffic|1907": {
            $sum: "$1907.IPV6Traffic"
        },
        "IPV6Traffic|1908": {
            $sum: "$1908.IPV6Traffic"
        },
        "IPV6Traffic|1909": {
            $sum: "$1909.IPV6Traffic"
        },
        "IPV6Traffic|1910": {
            $sum: "$1910.IPV6Traffic"
        },
        "IPV6Traffic|1911": {
            $sum: "$1911.IPV6Traffic"
        },
        "IPV6Traffic|1912": {
            $sum: "$1912.IPV6Traffic"
        },
        "IPV6Traffic|1913": {
            $sum: "$1913.IPV6Traffic"
        },
        "IPV6Traffic|1914": {
            $sum: "$1914.IPV6Traffic"
        },
        "IPV6Traffic|1915": {
            $sum: "$1915.IPV6Traffic"
        },
        "IPV6Traffic|1916": {
            $sum: "$1916.IPV6Traffic"
        },
        "IPV6Traffic|1917": {
            $sum: "$1917.IPV6Traffic"
        },
        "IPV6Traffic|1918": {
            $sum: "$1918.IPV6Traffic"
        },
        "IPV6Traffic|1919": {
            $sum: "$1919.IPV6Traffic"
        },
        "IPV6Traffic|1920": {
            $sum: "$1920.IPV6Traffic"
        },
        "IPV6Traffic|1921": {
            $sum: "$1921.IPV6Traffic"
        },
        "IPV6Traffic|1922": {
            $sum: "$1922.IPV6Traffic"
        },
        "IPV6Traffic|1923": {
            $sum: "$1923.IPV6Traffic"
        },
        "IPV6Traffic|1924": {
            $sum: "$1924.IPV6Traffic"
        },
        "IPV6Traffic|1925": {
            $sum: "$1925.IPV6Traffic"
        },
        "IPV6Traffic|1926": {
            $sum: "$1926.IPV6Traffic"
        },
        "IPV6Traffic|1927": {
            $sum: "$1927.IPV6Traffic"
        },
        "IPV6Traffic|1928": {
            $sum: "$1928.IPV6Traffic"
        },
        "IPV6Traffic|1929": {
            $sum: "$1929.IPV6Traffic"
        },
        "IPV6Traffic|1930": {
            $sum: "$1930.IPV6Traffic"
        },
        "IPV6Traffic|1931": {
            $sum: "$1931.IPV6Traffic"
        },
        "IPV6Traffic|1932": {
            $sum: "$1932.IPV6Traffic"
        },
        "IPV6Traffic|1933": {
            $sum: "$1933.IPV6Traffic"
        },
        "IPV6Traffic|1934": {
            $sum: "$1934.IPV6Traffic"
        },
        "IPV6Traffic|1935": {
            $sum: "$1935.IPV6Traffic"
        },
        "IPV6Traffic|1936": {
            $sum: "$1936.IPV6Traffic"
        },
        "IPV6Traffic|1937": {
            $sum: "$1937.IPV6Traffic"
        },
        "IPV6Traffic|1938": {
            $sum: "$1938.IPV6Traffic"
        },
        "IPV6Traffic|1939": {
            $sum: "$1939.IPV6Traffic"
        },
        "IPV6Traffic|1940": {
            $sum: "$1940.IPV6Traffic"
        },
        "IPV6Traffic|1941": {
            $sum: "$1941.IPV6Traffic"
        },
        "IPV6Traffic|1942": {
            $sum: "$1942.IPV6Traffic"
        },
        "IPV6Traffic|1943": {
            $sum: "$1943.IPV6Traffic"
        },
        "IPV6Traffic|1944": {
            $sum: "$1944.IPV6Traffic"
        },
        "IPV6Traffic|1945": {
            $sum: "$1945.IPV6Traffic"
        },
        "IPV6Traffic|1946": {
            $sum: "$1946.IPV6Traffic"
        },
        "IPV6Traffic|1947": {
            $sum: "$1947.IPV6Traffic"
        },
        "IPV6Traffic|1948": {
            $sum: "$1948.IPV6Traffic"
        },
        "IPV6Traffic|1949": {
            $sum: "$1949.IPV6Traffic"
        },
        "IPV6Traffic|1950": {
            $sum: "$1950.IPV6Traffic"
        },
        "IPV6Traffic|1951": {
            $sum: "$1951.IPV6Traffic"
        },
        "IPV6Traffic|1952": {
            $sum: "$1952.IPV6Traffic"
        },
        "IPV6Traffic|1953": {
            $sum: "$1953.IPV6Traffic"
        },
        "IPV6Traffic|1954": {
            $sum: "$1954.IPV6Traffic"
        },
        "IPV6Traffic|1955": {
            $sum: "$1955.IPV6Traffic"
        },
        "IPV6Traffic|1956": {
            $sum: "$1956.IPV6Traffic"
        },
        "IPV6Traffic|1957": {
            $sum: "$1957.IPV6Traffic"
        },
        "IPV6Traffic|1958": {
            $sum: "$1958.IPV6Traffic"
        },
        "IPV6Traffic|1959": {
            $sum: "$1959.IPV6Traffic"
        },
        "IPV6Traffic|2000": {
            $sum: "$2000.IPV6Traffic"
        },
        "IPV6Traffic|2001": {
            $sum: "$2001.IPV6Traffic"
        },
        "IPV6Traffic|2002": {
            $sum: "$2002.IPV6Traffic"
        },
        "IPV6Traffic|2003": {
            $sum: "$2003.IPV6Traffic"
        },
        "IPV6Traffic|2004": {
            $sum: "$2004.IPV6Traffic"
        },
        "IPV6Traffic|2005": {
            $sum: "$2005.IPV6Traffic"
        },
        "IPV6Traffic|2006": {
            $sum: "$2006.IPV6Traffic"
        },
        "IPV6Traffic|2007": {
            $sum: "$2007.IPV6Traffic"
        },
        "IPV6Traffic|2008": {
            $sum: "$2008.IPV6Traffic"
        },
        "IPV6Traffic|2009": {
            $sum: "$2009.IPV6Traffic"
        },
        "IPV6Traffic|2010": {
            $sum: "$2010.IPV6Traffic"
        },
        "IPV6Traffic|2011": {
            $sum: "$2011.IPV6Traffic"
        },
        "IPV6Traffic|2012": {
            $sum: "$2012.IPV6Traffic"
        },
        "IPV6Traffic|2013": {
            $sum: "$2013.IPV6Traffic"
        },
        "IPV6Traffic|2014": {
            $sum: "$2014.IPV6Traffic"
        },
        "IPV6Traffic|2015": {
            $sum: "$2015.IPV6Traffic"
        },
        "IPV6Traffic|2016": {
            $sum: "$2016.IPV6Traffic"
        },
        "IPV6Traffic|2017": {
            $sum: "$2017.IPV6Traffic"
        },
        "IPV6Traffic|2018": {
            $sum: "$2018.IPV6Traffic"
        },
        "IPV6Traffic|2019": {
            $sum: "$2019.IPV6Traffic"
        },
        "IPV6Traffic|2020": {
            $sum: "$2020.IPV6Traffic"
        },
        "IPV6Traffic|2021": {
            $sum: "$2021.IPV6Traffic"
        },
        "IPV6Traffic|2022": {
            $sum: "$2022.IPV6Traffic"
        },
        "IPV6Traffic|2023": {
            $sum: "$2023.IPV6Traffic"
        },
        "IPV6Traffic|2024": {
            $sum: "$2024.IPV6Traffic"
        },
        "IPV6Traffic|2025": {
            $sum: "$2025.IPV6Traffic"
        },
        "IPV6Traffic|2026": {
            $sum: "$2026.IPV6Traffic"
        },
        "IPV6Traffic|2027": {
            $sum: "$2027.IPV6Traffic"
        },
        "IPV6Traffic|2028": {
            $sum: "$2028.IPV6Traffic"
        },
        "IPV6Traffic|2029": {
            $sum: "$2029.IPV6Traffic"
        },
        "IPV6Traffic|2030": {
            $sum: "$2030.IPV6Traffic"
        },
        "IPV6Traffic|2031": {
            $sum: "$2031.IPV6Traffic"
        },
        "IPV6Traffic|2032": {
            $sum: "$2032.IPV6Traffic"
        },
        "IPV6Traffic|2033": {
            $sum: "$2033.IPV6Traffic"
        },
        "IPV6Traffic|2034": {
            $sum: "$2034.IPV6Traffic"
        },
        "IPV6Traffic|2035": {
            $sum: "$2035.IPV6Traffic"
        },
        "IPV6Traffic|2036": {
            $sum: "$2036.IPV6Traffic"
        },
        "IPV6Traffic|2037": {
            $sum: "$2037.IPV6Traffic"
        },
        "IPV6Traffic|2038": {
            $sum: "$2038.IPV6Traffic"
        },
        "IPV6Traffic|2039": {
            $sum: "$2039.IPV6Traffic"
        },
        "IPV6Traffic|2040": {
            $sum: "$2040.IPV6Traffic"
        },
        "IPV6Traffic|2041": {
            $sum: "$2041.IPV6Traffic"
        },
        "IPV6Traffic|2042": {
            $sum: "$2042.IPV6Traffic"
        },
        "IPV6Traffic|2043": {
            $sum: "$2043.IPV6Traffic"
        },
        "IPV6Traffic|2044": {
            $sum: "$2044.IPV6Traffic"
        },
        "IPV6Traffic|2045": {
            $sum: "$2045.IPV6Traffic"
        },
        "IPV6Traffic|2046": {
            $sum: "$2046.IPV6Traffic"
        },
        "IPV6Traffic|2047": {
            $sum: "$2047.IPV6Traffic"
        },
        "IPV6Traffic|2048": {
            $sum: "$2048.IPV6Traffic"
        },
        "IPV6Traffic|2049": {
            $sum: "$2049.IPV6Traffic"
        },
        "IPV6Traffic|2050": {
            $sum: "$2050.IPV6Traffic"
        },
        "IPV6Traffic|2051": {
            $sum: "$2051.IPV6Traffic"
        },
        "IPV6Traffic|2052": {
            $sum: "$2052.IPV6Traffic"
        },
        "IPV6Traffic|2053": {
            $sum: "$2053.IPV6Traffic"
        },
        "IPV6Traffic|2054": {
            $sum: "$2054.IPV6Traffic"
        },
        "IPV6Traffic|2055": {
            $sum: "$2055.IPV6Traffic"
        },
        "IPV6Traffic|2056": {
            $sum: "$2056.IPV6Traffic"
        },
        "IPV6Traffic|2057": {
            $sum: "$2057.IPV6Traffic"
        },
        "IPV6Traffic|2058": {
            $sum: "$2058.IPV6Traffic"
        },
        "IPV6Traffic|2059": {
            $sum: "$2059.IPV6Traffic"
        },
        "IPV6Traffic|2100": {
            $sum: "$2100.IPV6Traffic"
        },
        "IPV6Traffic|2101": {
            $sum: "$2101.IPV6Traffic"
        },
        "IPV6Traffic|2102": {
            $sum: "$2102.IPV6Traffic"
        },
        "IPV6Traffic|2103": {
            $sum: "$2103.IPV6Traffic"
        },
        "IPV6Traffic|2104": {
            $sum: "$2104.IPV6Traffic"
        },
        "IPV6Traffic|2105": {
            $sum: "$2105.IPV6Traffic"
        },
        "IPV6Traffic|2106": {
            $sum: "$2106.IPV6Traffic"
        },
        "IPV6Traffic|2107": {
            $sum: "$2107.IPV6Traffic"
        },
        "IPV6Traffic|2108": {
            $sum: "$2108.IPV6Traffic"
        },
        "IPV6Traffic|2109": {
            $sum: "$2109.IPV6Traffic"
        },
        "IPV6Traffic|2110": {
            $sum: "$2110.IPV6Traffic"
        },
        "IPV6Traffic|2111": {
            $sum: "$2111.IPV6Traffic"
        },
        "IPV6Traffic|2112": {
            $sum: "$2112.IPV6Traffic"
        },
        "IPV6Traffic|2113": {
            $sum: "$2113.IPV6Traffic"
        },
        "IPV6Traffic|2114": {
            $sum: "$2114.IPV6Traffic"
        },
        "IPV6Traffic|2115": {
            $sum: "$2115.IPV6Traffic"
        },
        "IPV6Traffic|2116": {
            $sum: "$2116.IPV6Traffic"
        },
        "IPV6Traffic|2117": {
            $sum: "$2117.IPV6Traffic"
        },
        "IPV6Traffic|2118": {
            $sum: "$2118.IPV6Traffic"
        },
        "IPV6Traffic|2119": {
            $sum: "$2119.IPV6Traffic"
        },
        "IPV6Traffic|2120": {
            $sum: "$2120.IPV6Traffic"
        },
        "IPV6Traffic|2121": {
            $sum: "$2121.IPV6Traffic"
        },
        "IPV6Traffic|2122": {
            $sum: "$2122.IPV6Traffic"
        },
        "IPV6Traffic|2123": {
            $sum: "$2123.IPV6Traffic"
        },
        "IPV6Traffic|2124": {
            $sum: "$2124.IPV6Traffic"
        },
        "IPV6Traffic|2125": {
            $sum: "$2125.IPV6Traffic"
        },
        "IPV6Traffic|2126": {
            $sum: "$2126.IPV6Traffic"
        },
        "IPV6Traffic|2127": {
            $sum: "$2127.IPV6Traffic"
        },
        "IPV6Traffic|2128": {
            $sum: "$2128.IPV6Traffic"
        },
        "IPV6Traffic|2129": {
            $sum: "$2129.IPV6Traffic"
        },
        "IPV6Traffic|2130": {
            $sum: "$2130.IPV6Traffic"
        },
        "IPV6Traffic|2131": {
            $sum: "$2131.IPV6Traffic"
        },
        "IPV6Traffic|2132": {
            $sum: "$2132.IPV6Traffic"
        },
        "IPV6Traffic|2133": {
            $sum: "$2133.IPV6Traffic"
        },
        "IPV6Traffic|2134": {
            $sum: "$2134.IPV6Traffic"
        },
        "IPV6Traffic|2135": {
            $sum: "$2135.IPV6Traffic"
        },
        "IPV6Traffic|2136": {
            $sum: "$2136.IPV6Traffic"
        },
        "IPV6Traffic|2137": {
            $sum: "$2137.IPV6Traffic"
        },
        "IPV6Traffic|2138": {
            $sum: "$2138.IPV6Traffic"
        },
        "IPV6Traffic|2139": {
            $sum: "$2139.IPV6Traffic"
        },
        "IPV6Traffic|2140": {
            $sum: "$2140.IPV6Traffic"
        },
        "IPV6Traffic|2141": {
            $sum: "$2141.IPV6Traffic"
        },
        "IPV6Traffic|2142": {
            $sum: "$2142.IPV6Traffic"
        },
        "IPV6Traffic|2143": {
            $sum: "$2143.IPV6Traffic"
        },
        "IPV6Traffic|2144": {
            $sum: "$2144.IPV6Traffic"
        },
        "IPV6Traffic|2145": {
            $sum: "$2145.IPV6Traffic"
        },
        "IPV6Traffic|2146": {
            $sum: "$2146.IPV6Traffic"
        },
        "IPV6Traffic|2147": {
            $sum: "$2147.IPV6Traffic"
        },
        "IPV6Traffic|2148": {
            $sum: "$2148.IPV6Traffic"
        },
        "IPV6Traffic|2149": {
            $sum: "$2149.IPV6Traffic"
        },
        "IPV6Traffic|2150": {
            $sum: "$2150.IPV6Traffic"
        },
        "IPV6Traffic|2151": {
            $sum: "$2151.IPV6Traffic"
        },
        "IPV6Traffic|2152": {
            $sum: "$2152.IPV6Traffic"
        },
        "IPV6Traffic|2153": {
            $sum: "$2153.IPV6Traffic"
        },
        "IPV6Traffic|2154": {
            $sum: "$2154.IPV6Traffic"
        },
        "IPV6Traffic|2155": {
            $sum: "$2155.IPV6Traffic"
        },
        "IPV6Traffic|2156": {
            $sum: "$2156.IPV6Traffic"
        },
        "IPV6Traffic|2157": {
            $sum: "$2157.IPV6Traffic"
        },
        "IPV6Traffic|2158": {
            $sum: "$2158.IPV6Traffic"
        },
        "IPV6Traffic|2159": {
            $sum: "$2159.IPV6Traffic"
        },
        "IPV6Traffic|2200": {
            $sum: "$2200.IPV6Traffic"
        },
        "IPV6Traffic|2201": {
            $sum: "$2201.IPV6Traffic"
        },
        "IPV6Traffic|2202": {
            $sum: "$2202.IPV6Traffic"
        },
        "IPV6Traffic|2203": {
            $sum: "$2203.IPV6Traffic"
        },
        "IPV6Traffic|2204": {
            $sum: "$2204.IPV6Traffic"
        },
        "IPV6Traffic|2205": {
            $sum: "$2205.IPV6Traffic"
        },
        "IPV6Traffic|2206": {
            $sum: "$2206.IPV6Traffic"
        },
        "IPV6Traffic|2207": {
            $sum: "$2207.IPV6Traffic"
        },
        "IPV6Traffic|2208": {
            $sum: "$2208.IPV6Traffic"
        },
        "IPV6Traffic|2209": {
            $sum: "$2209.IPV6Traffic"
        },
        "IPV6Traffic|2210": {
            $sum: "$2210.IPV6Traffic"
        },
        "IPV6Traffic|2211": {
            $sum: "$2211.IPV6Traffic"
        },
        "IPV6Traffic|2212": {
            $sum: "$2212.IPV6Traffic"
        },
        "IPV6Traffic|2213": {
            $sum: "$2213.IPV6Traffic"
        },
        "IPV6Traffic|2214": {
            $sum: "$2214.IPV6Traffic"
        },
        "IPV6Traffic|2215": {
            $sum: "$2215.IPV6Traffic"
        },
        "IPV6Traffic|2216": {
            $sum: "$2216.IPV6Traffic"
        },
        "IPV6Traffic|2217": {
            $sum: "$2217.IPV6Traffic"
        },
        "IPV6Traffic|2218": {
            $sum: "$2218.IPV6Traffic"
        },
        "IPV6Traffic|2219": {
            $sum: "$2219.IPV6Traffic"
        },
        "IPV6Traffic|2220": {
            $sum: "$2220.IPV6Traffic"
        },
        "IPV6Traffic|2221": {
            $sum: "$2221.IPV6Traffic"
        },
        "IPV6Traffic|2222": {
            $sum: "$2222.IPV6Traffic"
        },
        "IPV6Traffic|2223": {
            $sum: "$2223.IPV6Traffic"
        },
        "IPV6Traffic|2224": {
            $sum: "$2224.IPV6Traffic"
        },
        "IPV6Traffic|2225": {
            $sum: "$2225.IPV6Traffic"
        },
        "IPV6Traffic|2226": {
            $sum: "$2226.IPV6Traffic"
        },
        "IPV6Traffic|2227": {
            $sum: "$2227.IPV6Traffic"
        },
        "IPV6Traffic|2228": {
            $sum: "$2228.IPV6Traffic"
        },
        "IPV6Traffic|2229": {
            $sum: "$2229.IPV6Traffic"
        },
        "IPV6Traffic|2230": {
            $sum: "$2230.IPV6Traffic"
        },
        "IPV6Traffic|2231": {
            $sum: "$2231.IPV6Traffic"
        },
        "IPV6Traffic|2232": {
            $sum: "$2232.IPV6Traffic"
        },
        "IPV6Traffic|2233": {
            $sum: "$2233.IPV6Traffic"
        },
        "IPV6Traffic|2234": {
            $sum: "$2234.IPV6Traffic"
        },
        "IPV6Traffic|2235": {
            $sum: "$2235.IPV6Traffic"
        },
        "IPV6Traffic|2236": {
            $sum: "$2236.IPV6Traffic"
        },
        "IPV6Traffic|2237": {
            $sum: "$2237.IPV6Traffic"
        },
        "IPV6Traffic|2238": {
            $sum: "$2238.IPV6Traffic"
        },
        "IPV6Traffic|2239": {
            $sum: "$2239.IPV6Traffic"
        },
        "IPV6Traffic|2240": {
            $sum: "$2240.IPV6Traffic"
        },
        "IPV6Traffic|2241": {
            $sum: "$2241.IPV6Traffic"
        },
        "IPV6Traffic|2242": {
            $sum: "$2242.IPV6Traffic"
        },
        "IPV6Traffic|2243": {
            $sum: "$2243.IPV6Traffic"
        },
        "IPV6Traffic|2244": {
            $sum: "$2244.IPV6Traffic"
        },
        "IPV6Traffic|2245": {
            $sum: "$2245.IPV6Traffic"
        },
        "IPV6Traffic|2246": {
            $sum: "$2246.IPV6Traffic"
        },
        "IPV6Traffic|2247": {
            $sum: "$2247.IPV6Traffic"
        },
        "IPV6Traffic|2248": {
            $sum: "$2248.IPV6Traffic"
        },
        "IPV6Traffic|2249": {
            $sum: "$2249.IPV6Traffic"
        },
        "IPV6Traffic|2250": {
            $sum: "$2250.IPV6Traffic"
        },
        "IPV6Traffic|2251": {
            $sum: "$2251.IPV6Traffic"
        },
        "IPV6Traffic|2252": {
            $sum: "$2252.IPV6Traffic"
        },
        "IPV6Traffic|2253": {
            $sum: "$2253.IPV6Traffic"
        },
        "IPV6Traffic|2254": {
            $sum: "$2254.IPV6Traffic"
        },
        "IPV6Traffic|2255": {
            $sum: "$2255.IPV6Traffic"
        },
        "IPV6Traffic|2256": {
            $sum: "$2256.IPV6Traffic"
        },
        "IPV6Traffic|2257": {
            $sum: "$2257.IPV6Traffic"
        },
        "IPV6Traffic|2258": {
            $sum: "$2258.IPV6Traffic"
        },
        "IPV6Traffic|2259": {
            $sum: "$2259.IPV6Traffic"
        },
        "IPV6Traffic|2300": {
            $sum: "$2300.IPV6Traffic"
        },
        "IPV6Traffic|2301": {
            $sum: "$2301.IPV6Traffic"
        },
        "IPV6Traffic|2302": {
            $sum: "$2302.IPV6Traffic"
        },
        "IPV6Traffic|2303": {
            $sum: "$2303.IPV6Traffic"
        },
        "IPV6Traffic|2304": {
            $sum: "$2304.IPV6Traffic"
        },
        "IPV6Traffic|2305": {
            $sum: "$2305.IPV6Traffic"
        },
        "IPV6Traffic|2306": {
            $sum: "$2306.IPV6Traffic"
        },
        "IPV6Traffic|2307": {
            $sum: "$2307.IPV6Traffic"
        },
        "IPV6Traffic|2308": {
            $sum: "$2308.IPV6Traffic"
        },
        "IPV6Traffic|2309": {
            $sum: "$2309.IPV6Traffic"
        },
        "IPV6Traffic|2310": {
            $sum: "$2310.IPV6Traffic"
        },
        "IPV6Traffic|2311": {
            $sum: "$2311.IPV6Traffic"
        },
        "IPV6Traffic|2312": {
            $sum: "$2312.IPV6Traffic"
        },
        "IPV6Traffic|2313": {
            $sum: "$2313.IPV6Traffic"
        },
        "IPV6Traffic|2314": {
            $sum: "$2314.IPV6Traffic"
        },
        "IPV6Traffic|2315": {
            $sum: "$2315.IPV6Traffic"
        },
        "IPV6Traffic|2316": {
            $sum: "$2316.IPV6Traffic"
        },
        "IPV6Traffic|2317": {
            $sum: "$2317.IPV6Traffic"
        },
        "IPV6Traffic|2318": {
            $sum: "$2318.IPV6Traffic"
        },
        "IPV6Traffic|2319": {
            $sum: "$2319.IPV6Traffic"
        },
        "IPV6Traffic|2320": {
            $sum: "$2320.IPV6Traffic"
        },
        "IPV6Traffic|2321": {
            $sum: "$2321.IPV6Traffic"
        },
        "IPV6Traffic|2322": {
            $sum: "$2322.IPV6Traffic"
        },
        "IPV6Traffic|2323": {
            $sum: "$2323.IPV6Traffic"
        },
        "IPV6Traffic|2324": {
            $sum: "$2324.IPV6Traffic"
        },
        "IPV6Traffic|2325": {
            $sum: "$2325.IPV6Traffic"
        },
        "IPV6Traffic|2326": {
            $sum: "$2326.IPV6Traffic"
        },
        "IPV6Traffic|2327": {
            $sum: "$2327.IPV6Traffic"
        },
        "IPV6Traffic|2328": {
            $sum: "$2328.IPV6Traffic"
        },
        "IPV6Traffic|2329": {
            $sum: "$2329.IPV6Traffic"
        },
        "IPV6Traffic|2330": {
            $sum: "$2330.IPV6Traffic"
        },
        "IPV6Traffic|2331": {
            $sum: "$2331.IPV6Traffic"
        },
        "IPV6Traffic|2332": {
            $sum: "$2332.IPV6Traffic"
        },
        "IPV6Traffic|2333": {
            $sum: "$2333.IPV6Traffic"
        },
        "IPV6Traffic|2334": {
            $sum: "$2334.IPV6Traffic"
        },
        "IPV6Traffic|2335": {
            $sum: "$2335.IPV6Traffic"
        },
        "IPV6Traffic|2336": {
            $sum: "$2336.IPV6Traffic"
        },
        "IPV6Traffic|2337": {
            $sum: "$2337.IPV6Traffic"
        },
        "IPV6Traffic|2338": {
            $sum: "$2338.IPV6Traffic"
        },
        "IPV6Traffic|2339": {
            $sum: "$2339.IPV6Traffic"
        },
        "IPV6Traffic|2340": {
            $sum: "$2340.IPV6Traffic"
        },
        "IPV6Traffic|2341": {
            $sum: "$2341.IPV6Traffic"
        },
        "IPV6Traffic|2342": {
            $sum: "$2342.IPV6Traffic"
        },
        "IPV6Traffic|2343": {
            $sum: "$2343.IPV6Traffic"
        },
        "IPV6Traffic|2344": {
            $sum: "$2344.IPV6Traffic"
        },
        "IPV6Traffic|2345": {
            $sum: "$2345.IPV6Traffic"
        },
        "IPV6Traffic|2346": {
            $sum: "$2346.IPV6Traffic"
        },
        "IPV6Traffic|2347": {
            $sum: "$2347.IPV6Traffic"
        },
        "IPV6Traffic|2348": {
            $sum: "$2348.IPV6Traffic"
        },
        "IPV6Traffic|2349": {
            $sum: "$2349.IPV6Traffic"
        },
        "IPV6Traffic|2350": {
            $sum: "$2350.IPV6Traffic"
        },
        "IPV6Traffic|2351": {
            $sum: "$2351.IPV6Traffic"
        },
        "IPV6Traffic|2352": {
            $sum: "$2352.IPV6Traffic"
        },
        "IPV6Traffic|2353": {
            $sum: "$2353.IPV6Traffic"
        },
        "IPV6Traffic|2354": {
            $sum: "$2354.IPV6Traffic"
        },
        "IPV6Traffic|2355": {
            $sum: "$2355.IPV6Traffic"
        },
        "IPV6Traffic|2356": {
            $sum: "$2356.IPV6Traffic"
        },
        "IPV6Traffic|2357": {
            $sum: "$2357.IPV6Traffic"
        },
        "IPV6Traffic|2358": {
            $sum: "$2358.IPV6Traffic"
        },
        "IPV6Traffic|2359": {
            $sum: "$2359.IPV6Traffic"
        },
        "PassTraffic|0000": {
            $sum: "$0000.PassTraffic"
        },
        "PassTraffic|0001": {
            $sum: "$0001.PassTraffic"
        },
        "PassTraffic|0002": {
            $sum: "$0002.PassTraffic"
        },
        "PassTraffic|0003": {
            $sum: "$0003.PassTraffic"
        },
        "PassTraffic|0004": {
            $sum: "$0004.PassTraffic"
        },
        "PassTraffic|0005": {
            $sum: "$0005.PassTraffic"
        },
        "PassTraffic|0006": {
            $sum: "$0006.PassTraffic"
        },
        "PassTraffic|0007": {
            $sum: "$0007.PassTraffic"
        },
        "PassTraffic|0008": {
            $sum: "$0008.PassTraffic"
        },
        "PassTraffic|0009": {
            $sum: "$0009.PassTraffic"
        },
        "PassTraffic|0010": {
            $sum: "$0010.PassTraffic"
        },
        "PassTraffic|0011": {
            $sum: "$0011.PassTraffic"
        },
        "PassTraffic|0012": {
            $sum: "$0012.PassTraffic"
        },
        "PassTraffic|0013": {
            $sum: "$0013.PassTraffic"
        },
        "PassTraffic|0014": {
            $sum: "$0014.PassTraffic"
        },
        "PassTraffic|0015": {
            $sum: "$0015.PassTraffic"
        },
        "PassTraffic|0016": {
            $sum: "$0016.PassTraffic"
        },
        "PassTraffic|0017": {
            $sum: "$0017.PassTraffic"
        },
        "PassTraffic|0018": {
            $sum: "$0018.PassTraffic"
        },
        "PassTraffic|0019": {
            $sum: "$0019.PassTraffic"
        },
        "PassTraffic|0020": {
            $sum: "$0020.PassTraffic"
        },
        "PassTraffic|0021": {
            $sum: "$0021.PassTraffic"
        },
        "PassTraffic|0022": {
            $sum: "$0022.PassTraffic"
        },
        "PassTraffic|0023": {
            $sum: "$0023.PassTraffic"
        },
        "PassTraffic|0024": {
            $sum: "$0024.PassTraffic"
        },
        "PassTraffic|0025": {
            $sum: "$0025.PassTraffic"
        },
        "PassTraffic|0026": {
            $sum: "$0026.PassTraffic"
        },
        "PassTraffic|0027": {
            $sum: "$0027.PassTraffic"
        },
        "PassTraffic|0028": {
            $sum: "$0028.PassTraffic"
        },
        "PassTraffic|0029": {
            $sum: "$0029.PassTraffic"
        },
        "PassTraffic|0030": {
            $sum: "$0030.PassTraffic"
        },
        "PassTraffic|0031": {
            $sum: "$0031.PassTraffic"
        },
        "PassTraffic|0032": {
            $sum: "$0032.PassTraffic"
        },
        "PassTraffic|0033": {
            $sum: "$0033.PassTraffic"
        },
        "PassTraffic|0034": {
            $sum: "$0034.PassTraffic"
        },
        "PassTraffic|0035": {
            $sum: "$0035.PassTraffic"
        },
        "PassTraffic|0036": {
            $sum: "$0036.PassTraffic"
        },
        "PassTraffic|0037": {
            $sum: "$0037.PassTraffic"
        },
        "PassTraffic|0038": {
            $sum: "$0038.PassTraffic"
        },
        "PassTraffic|0039": {
            $sum: "$0039.PassTraffic"
        },
        "PassTraffic|0040": {
            $sum: "$0040.PassTraffic"
        },
        "PassTraffic|0041": {
            $sum: "$0041.PassTraffic"
        },
        "PassTraffic|0042": {
            $sum: "$0042.PassTraffic"
        },
        "PassTraffic|0043": {
            $sum: "$0043.PassTraffic"
        },
        "PassTraffic|0044": {
            $sum: "$0044.PassTraffic"
        },
        "PassTraffic|0045": {
            $sum: "$0045.PassTraffic"
        },
        "PassTraffic|0046": {
            $sum: "$0046.PassTraffic"
        },
        "PassTraffic|0047": {
            $sum: "$0047.PassTraffic"
        },
        "PassTraffic|0048": {
            $sum: "$0048.PassTraffic"
        },
        "PassTraffic|0049": {
            $sum: "$0049.PassTraffic"
        },
        "PassTraffic|0050": {
            $sum: "$0050.PassTraffic"
        },
        "PassTraffic|0051": {
            $sum: "$0051.PassTraffic"
        },
        "PassTraffic|0052": {
            $sum: "$0052.PassTraffic"
        },
        "PassTraffic|0053": {
            $sum: "$0053.PassTraffic"
        },
        "PassTraffic|0054": {
            $sum: "$0054.PassTraffic"
        },
        "PassTraffic|0055": {
            $sum: "$0055.PassTraffic"
        },
        "PassTraffic|0056": {
            $sum: "$0056.PassTraffic"
        },
        "PassTraffic|0057": {
            $sum: "$0057.PassTraffic"
        },
        "PassTraffic|0058": {
            $sum: "$0058.PassTraffic"
        },
        "PassTraffic|0059": {
            $sum: "$0059.PassTraffic"
        },
        "PassTraffic|0100": {
            $sum: "$0100.PassTraffic"
        },
        "PassTraffic|0101": {
            $sum: "$0101.PassTraffic"
        },
        "PassTraffic|0102": {
            $sum: "$0102.PassTraffic"
        },
        "PassTraffic|0103": {
            $sum: "$0103.PassTraffic"
        },
        "PassTraffic|0104": {
            $sum: "$0104.PassTraffic"
        },
        "PassTraffic|0105": {
            $sum: "$0105.PassTraffic"
        },
        "PassTraffic|0106": {
            $sum: "$0106.PassTraffic"
        },
        "PassTraffic|0107": {
            $sum: "$0107.PassTraffic"
        },
        "PassTraffic|0108": {
            $sum: "$0108.PassTraffic"
        },
        "PassTraffic|0109": {
            $sum: "$0109.PassTraffic"
        },
        "PassTraffic|0110": {
            $sum: "$0110.PassTraffic"
        },
        "PassTraffic|0111": {
            $sum: "$0111.PassTraffic"
        },
        "PassTraffic|0112": {
            $sum: "$0112.PassTraffic"
        },
        "PassTraffic|0113": {
            $sum: "$0113.PassTraffic"
        },
        "PassTraffic|0114": {
            $sum: "$0114.PassTraffic"
        },
        "PassTraffic|0115": {
            $sum: "$0115.PassTraffic"
        },
        "PassTraffic|0116": {
            $sum: "$0116.PassTraffic"
        },
        "PassTraffic|0117": {
            $sum: "$0117.PassTraffic"
        },
        "PassTraffic|0118": {
            $sum: "$0118.PassTraffic"
        },
        "PassTraffic|0119": {
            $sum: "$0119.PassTraffic"
        },
        "PassTraffic|0120": {
            $sum: "$0120.PassTraffic"
        },
        "PassTraffic|0121": {
            $sum: "$0121.PassTraffic"
        },
        "PassTraffic|0122": {
            $sum: "$0122.PassTraffic"
        },
        "PassTraffic|0123": {
            $sum: "$0123.PassTraffic"
        },
        "PassTraffic|0124": {
            $sum: "$0124.PassTraffic"
        },
        "PassTraffic|0125": {
            $sum: "$0125.PassTraffic"
        },
        "PassTraffic|0126": {
            $sum: "$0126.PassTraffic"
        },
        "PassTraffic|0127": {
            $sum: "$0127.PassTraffic"
        },
        "PassTraffic|0128": {
            $sum: "$0128.PassTraffic"
        },
        "PassTraffic|0129": {
            $sum: "$0129.PassTraffic"
        },
        "PassTraffic|0130": {
            $sum: "$0130.PassTraffic"
        },
        "PassTraffic|0131": {
            $sum: "$0131.PassTraffic"
        },
        "PassTraffic|0132": {
            $sum: "$0132.PassTraffic"
        },
        "PassTraffic|0133": {
            $sum: "$0133.PassTraffic"
        },
        "PassTraffic|0134": {
            $sum: "$0134.PassTraffic"
        },
        "PassTraffic|0135": {
            $sum: "$0135.PassTraffic"
        },
        "PassTraffic|0136": {
            $sum: "$0136.PassTraffic"
        },
        "PassTraffic|0137": {
            $sum: "$0137.PassTraffic"
        },
        "PassTraffic|0138": {
            $sum: "$0138.PassTraffic"
        },
        "PassTraffic|0139": {
            $sum: "$0139.PassTraffic"
        },
        "PassTraffic|0140": {
            $sum: "$0140.PassTraffic"
        },
        "PassTraffic|0141": {
            $sum: "$0141.PassTraffic"
        },
        "PassTraffic|0142": {
            $sum: "$0142.PassTraffic"
        },
        "PassTraffic|0143": {
            $sum: "$0143.PassTraffic"
        },
        "PassTraffic|0144": {
            $sum: "$0144.PassTraffic"
        },
        "PassTraffic|0145": {
            $sum: "$0145.PassTraffic"
        },
        "PassTraffic|0146": {
            $sum: "$0146.PassTraffic"
        },
        "PassTraffic|0147": {
            $sum: "$0147.PassTraffic"
        },
        "PassTraffic|0148": {
            $sum: "$0148.PassTraffic"
        },
        "PassTraffic|0149": {
            $sum: "$0149.PassTraffic"
        },
        "PassTraffic|0150": {
            $sum: "$0150.PassTraffic"
        },
        "PassTraffic|0151": {
            $sum: "$0151.PassTraffic"
        },
        "PassTraffic|0152": {
            $sum: "$0152.PassTraffic"
        },
        "PassTraffic|0153": {
            $sum: "$0153.PassTraffic"
        },
        "PassTraffic|0154": {
            $sum: "$0154.PassTraffic"
        },
        "PassTraffic|0155": {
            $sum: "$0155.PassTraffic"
        },
        "PassTraffic|0156": {
            $sum: "$0156.PassTraffic"
        },
        "PassTraffic|0157": {
            $sum: "$0157.PassTraffic"
        },
        "PassTraffic|0158": {
            $sum: "$0158.PassTraffic"
        },
        "PassTraffic|0159": {
            $sum: "$0159.PassTraffic"
        },
        "PassTraffic|0200": {
            $sum: "$0200.PassTraffic"
        },
        "PassTraffic|0201": {
            $sum: "$0201.PassTraffic"
        },
        "PassTraffic|0202": {
            $sum: "$0202.PassTraffic"
        },
        "PassTraffic|0203": {
            $sum: "$0203.PassTraffic"
        },
        "PassTraffic|0204": {
            $sum: "$0204.PassTraffic"
        },
        "PassTraffic|0205": {
            $sum: "$0205.PassTraffic"
        },
        "PassTraffic|0206": {
            $sum: "$0206.PassTraffic"
        },
        "PassTraffic|0207": {
            $sum: "$0207.PassTraffic"
        },
        "PassTraffic|0208": {
            $sum: "$0208.PassTraffic"
        },
        "PassTraffic|0209": {
            $sum: "$0209.PassTraffic"
        },
        "PassTraffic|0210": {
            $sum: "$0210.PassTraffic"
        },
        "PassTraffic|0211": {
            $sum: "$0211.PassTraffic"
        },
        "PassTraffic|0212": {
            $sum: "$0212.PassTraffic"
        },
        "PassTraffic|0213": {
            $sum: "$0213.PassTraffic"
        },
        "PassTraffic|0214": {
            $sum: "$0214.PassTraffic"
        },
        "PassTraffic|0215": {
            $sum: "$0215.PassTraffic"
        },
        "PassTraffic|0216": {
            $sum: "$0216.PassTraffic"
        },
        "PassTraffic|0217": {
            $sum: "$0217.PassTraffic"
        },
        "PassTraffic|0218": {
            $sum: "$0218.PassTraffic"
        },
        "PassTraffic|0219": {
            $sum: "$0219.PassTraffic"
        },
        "PassTraffic|0220": {
            $sum: "$0220.PassTraffic"
        },
        "PassTraffic|0221": {
            $sum: "$0221.PassTraffic"
        },
        "PassTraffic|0222": {
            $sum: "$0222.PassTraffic"
        },
        "PassTraffic|0223": {
            $sum: "$0223.PassTraffic"
        },
        "PassTraffic|0224": {
            $sum: "$0224.PassTraffic"
        },
        "PassTraffic|0225": {
            $sum: "$0225.PassTraffic"
        },
        "PassTraffic|0226": {
            $sum: "$0226.PassTraffic"
        },
        "PassTraffic|0227": {
            $sum: "$0227.PassTraffic"
        },
        "PassTraffic|0228": {
            $sum: "$0228.PassTraffic"
        },
        "PassTraffic|0229": {
            $sum: "$0229.PassTraffic"
        },
        "PassTraffic|0230": {
            $sum: "$0230.PassTraffic"
        },
        "PassTraffic|0231": {
            $sum: "$0231.PassTraffic"
        },
        "PassTraffic|0232": {
            $sum: "$0232.PassTraffic"
        },
        "PassTraffic|0233": {
            $sum: "$0233.PassTraffic"
        },
        "PassTraffic|0234": {
            $sum: "$0234.PassTraffic"
        },
        "PassTraffic|0235": {
            $sum: "$0235.PassTraffic"
        },
        "PassTraffic|0236": {
            $sum: "$0236.PassTraffic"
        },
        "PassTraffic|0237": {
            $sum: "$0237.PassTraffic"
        },
        "PassTraffic|0238": {
            $sum: "$0238.PassTraffic"
        },
        "PassTraffic|0239": {
            $sum: "$0239.PassTraffic"
        },
        "PassTraffic|0240": {
            $sum: "$0240.PassTraffic"
        },
        "PassTraffic|0241": {
            $sum: "$0241.PassTraffic"
        },
        "PassTraffic|0242": {
            $sum: "$0242.PassTraffic"
        },
        "PassTraffic|0243": {
            $sum: "$0243.PassTraffic"
        },
        "PassTraffic|0244": {
            $sum: "$0244.PassTraffic"
        },
        "PassTraffic|0245": {
            $sum: "$0245.PassTraffic"
        },
        "PassTraffic|0246": {
            $sum: "$0246.PassTraffic"
        },
        "PassTraffic|0247": {
            $sum: "$0247.PassTraffic"
        },
        "PassTraffic|0248": {
            $sum: "$0248.PassTraffic"
        },
        "PassTraffic|0249": {
            $sum: "$0249.PassTraffic"
        },
        "PassTraffic|0250": {
            $sum: "$0250.PassTraffic"
        },
        "PassTraffic|0251": {
            $sum: "$0251.PassTraffic"
        },
        "PassTraffic|0252": {
            $sum: "$0252.PassTraffic"
        },
        "PassTraffic|0253": {
            $sum: "$0253.PassTraffic"
        },
        "PassTraffic|0254": {
            $sum: "$0254.PassTraffic"
        },
        "PassTraffic|0255": {
            $sum: "$0255.PassTraffic"
        },
        "PassTraffic|0256": {
            $sum: "$0256.PassTraffic"
        },
        "PassTraffic|0257": {
            $sum: "$0257.PassTraffic"
        },
        "PassTraffic|0258": {
            $sum: "$0258.PassTraffic"
        },
        "PassTraffic|0259": {
            $sum: "$0259.PassTraffic"
        },
        "PassTraffic|0300": {
            $sum: "$0300.PassTraffic"
        },
        "PassTraffic|0301": {
            $sum: "$0301.PassTraffic"
        },
        "PassTraffic|0302": {
            $sum: "$0302.PassTraffic"
        },
        "PassTraffic|0303": {
            $sum: "$0303.PassTraffic"
        },
        "PassTraffic|0304": {
            $sum: "$0304.PassTraffic"
        },
        "PassTraffic|0305": {
            $sum: "$0305.PassTraffic"
        },
        "PassTraffic|0306": {
            $sum: "$0306.PassTraffic"
        },
        "PassTraffic|0307": {
            $sum: "$0307.PassTraffic"
        },
        "PassTraffic|0308": {
            $sum: "$0308.PassTraffic"
        },
        "PassTraffic|0309": {
            $sum: "$0309.PassTraffic"
        },
        "PassTraffic|0310": {
            $sum: "$0310.PassTraffic"
        },
        "PassTraffic|0311": {
            $sum: "$0311.PassTraffic"
        },
        "PassTraffic|0312": {
            $sum: "$0312.PassTraffic"
        },
        "PassTraffic|0313": {
            $sum: "$0313.PassTraffic"
        },
        "PassTraffic|0314": {
            $sum: "$0314.PassTraffic"
        },
        "PassTraffic|0315": {
            $sum: "$0315.PassTraffic"
        },
        "PassTraffic|0316": {
            $sum: "$0316.PassTraffic"
        },
        "PassTraffic|0317": {
            $sum: "$0317.PassTraffic"
        },
        "PassTraffic|0318": {
            $sum: "$0318.PassTraffic"
        },
        "PassTraffic|0319": {
            $sum: "$0319.PassTraffic"
        },
        "PassTraffic|0320": {
            $sum: "$0320.PassTraffic"
        },
        "PassTraffic|0321": {
            $sum: "$0321.PassTraffic"
        },
        "PassTraffic|0322": {
            $sum: "$0322.PassTraffic"
        },
        "PassTraffic|0323": {
            $sum: "$0323.PassTraffic"
        },
        "PassTraffic|0324": {
            $sum: "$0324.PassTraffic"
        },
        "PassTraffic|0325": {
            $sum: "$0325.PassTraffic"
        },
        "PassTraffic|0326": {
            $sum: "$0326.PassTraffic"
        },
        "PassTraffic|0327": {
            $sum: "$0327.PassTraffic"
        },
        "PassTraffic|0328": {
            $sum: "$0328.PassTraffic"
        },
        "PassTraffic|0329": {
            $sum: "$0329.PassTraffic"
        },
        "PassTraffic|0330": {
            $sum: "$0330.PassTraffic"
        },
        "PassTraffic|0331": {
            $sum: "$0331.PassTraffic"
        },
        "PassTraffic|0332": {
            $sum: "$0332.PassTraffic"
        },
        "PassTraffic|0333": {
            $sum: "$0333.PassTraffic"
        },
        "PassTraffic|0334": {
            $sum: "$0334.PassTraffic"
        },
        "PassTraffic|0335": {
            $sum: "$0335.PassTraffic"
        },
        "PassTraffic|0336": {
            $sum: "$0336.PassTraffic"
        },
        "PassTraffic|0337": {
            $sum: "$0337.PassTraffic"
        },
        "PassTraffic|0338": {
            $sum: "$0338.PassTraffic"
        },
        "PassTraffic|0339": {
            $sum: "$0339.PassTraffic"
        },
        "PassTraffic|0340": {
            $sum: "$0340.PassTraffic"
        },
        "PassTraffic|0341": {
            $sum: "$0341.PassTraffic"
        },
        "PassTraffic|0342": {
            $sum: "$0342.PassTraffic"
        },
        "PassTraffic|0343": {
            $sum: "$0343.PassTraffic"
        },
        "PassTraffic|0344": {
            $sum: "$0344.PassTraffic"
        },
        "PassTraffic|0345": {
            $sum: "$0345.PassTraffic"
        },
        "PassTraffic|0346": {
            $sum: "$0346.PassTraffic"
        },
        "PassTraffic|0347": {
            $sum: "$0347.PassTraffic"
        },
        "PassTraffic|0348": {
            $sum: "$0348.PassTraffic"
        },
        "PassTraffic|0349": {
            $sum: "$0349.PassTraffic"
        },
        "PassTraffic|0350": {
            $sum: "$0350.PassTraffic"
        },
        "PassTraffic|0351": {
            $sum: "$0351.PassTraffic"
        },
        "PassTraffic|0352": {
            $sum: "$0352.PassTraffic"
        },
        "PassTraffic|0353": {
            $sum: "$0353.PassTraffic"
        },
        "PassTraffic|0354": {
            $sum: "$0354.PassTraffic"
        },
        "PassTraffic|0355": {
            $sum: "$0355.PassTraffic"
        },
        "PassTraffic|0356": {
            $sum: "$0356.PassTraffic"
        },
        "PassTraffic|0357": {
            $sum: "$0357.PassTraffic"
        },
        "PassTraffic|0358": {
            $sum: "$0358.PassTraffic"
        },
        "PassTraffic|0359": {
            $sum: "$0359.PassTraffic"
        },
        "PassTraffic|0400": {
            $sum: "$0400.PassTraffic"
        },
        "PassTraffic|0401": {
            $sum: "$0401.PassTraffic"
        },
        "PassTraffic|0402": {
            $sum: "$0402.PassTraffic"
        },
        "PassTraffic|0403": {
            $sum: "$0403.PassTraffic"
        },
        "PassTraffic|0404": {
            $sum: "$0404.PassTraffic"
        },
        "PassTraffic|0405": {
            $sum: "$0405.PassTraffic"
        },
        "PassTraffic|0406": {
            $sum: "$0406.PassTraffic"
        },
        "PassTraffic|0407": {
            $sum: "$0407.PassTraffic"
        },
        "PassTraffic|0408": {
            $sum: "$0408.PassTraffic"
        },
        "PassTraffic|0409": {
            $sum: "$0409.PassTraffic"
        },
        "PassTraffic|0410": {
            $sum: "$0410.PassTraffic"
        },
        "PassTraffic|0411": {
            $sum: "$0411.PassTraffic"
        },
        "PassTraffic|0412": {
            $sum: "$0412.PassTraffic"
        },
        "PassTraffic|0413": {
            $sum: "$0413.PassTraffic"
        },
        "PassTraffic|0414": {
            $sum: "$0414.PassTraffic"
        },
        "PassTraffic|0415": {
            $sum: "$0415.PassTraffic"
        },
        "PassTraffic|0416": {
            $sum: "$0416.PassTraffic"
        },
        "PassTraffic|0417": {
            $sum: "$0417.PassTraffic"
        },
        "PassTraffic|0418": {
            $sum: "$0418.PassTraffic"
        },
        "PassTraffic|0419": {
            $sum: "$0419.PassTraffic"
        },
        "PassTraffic|0420": {
            $sum: "$0420.PassTraffic"
        },
        "PassTraffic|0421": {
            $sum: "$0421.PassTraffic"
        },
        "PassTraffic|0422": {
            $sum: "$0422.PassTraffic"
        },
        "PassTraffic|0423": {
            $sum: "$0423.PassTraffic"
        },
        "PassTraffic|0424": {
            $sum: "$0424.PassTraffic"
        },
        "PassTraffic|0425": {
            $sum: "$0425.PassTraffic"
        },
        "PassTraffic|0426": {
            $sum: "$0426.PassTraffic"
        },
        "PassTraffic|0427": {
            $sum: "$0427.PassTraffic"
        },
        "PassTraffic|0428": {
            $sum: "$0428.PassTraffic"
        },
        "PassTraffic|0429": {
            $sum: "$0429.PassTraffic"
        },
        "PassTraffic|0430": {
            $sum: "$0430.PassTraffic"
        },
        "PassTraffic|0431": {
            $sum: "$0431.PassTraffic"
        },
        "PassTraffic|0432": {
            $sum: "$0432.PassTraffic"
        },
        "PassTraffic|0433": {
            $sum: "$0433.PassTraffic"
        },
        "PassTraffic|0434": {
            $sum: "$0434.PassTraffic"
        },
        "PassTraffic|0435": {
            $sum: "$0435.PassTraffic"
        },
        "PassTraffic|0436": {
            $sum: "$0436.PassTraffic"
        },
        "PassTraffic|0437": {
            $sum: "$0437.PassTraffic"
        },
        "PassTraffic|0438": {
            $sum: "$0438.PassTraffic"
        },
        "PassTraffic|0439": {
            $sum: "$0439.PassTraffic"
        },
        "PassTraffic|0440": {
            $sum: "$0440.PassTraffic"
        },
        "PassTraffic|0441": {
            $sum: "$0441.PassTraffic"
        },
        "PassTraffic|0442": {
            $sum: "$0442.PassTraffic"
        },
        "PassTraffic|0443": {
            $sum: "$0443.PassTraffic"
        },
        "PassTraffic|0444": {
            $sum: "$0444.PassTraffic"
        },
        "PassTraffic|0445": {
            $sum: "$0445.PassTraffic"
        },
        "PassTraffic|0446": {
            $sum: "$0446.PassTraffic"
        },
        "PassTraffic|0447": {
            $sum: "$0447.PassTraffic"
        },
        "PassTraffic|0448": {
            $sum: "$0448.PassTraffic"
        },
        "PassTraffic|0449": {
            $sum: "$0449.PassTraffic"
        },
        "PassTraffic|0450": {
            $sum: "$0450.PassTraffic"
        },
        "PassTraffic|0451": {
            $sum: "$0451.PassTraffic"
        },
        "PassTraffic|0452": {
            $sum: "$0452.PassTraffic"
        },
        "PassTraffic|0453": {
            $sum: "$0453.PassTraffic"
        },
        "PassTraffic|0454": {
            $sum: "$0454.PassTraffic"
        },
        "PassTraffic|0455": {
            $sum: "$0455.PassTraffic"
        },
        "PassTraffic|0456": {
            $sum: "$0456.PassTraffic"
        },
        "PassTraffic|0457": {
            $sum: "$0457.PassTraffic"
        },
        "PassTraffic|0458": {
            $sum: "$0458.PassTraffic"
        },
        "PassTraffic|0459": {
            $sum: "$0459.PassTraffic"
        },
        "PassTraffic|0500": {
            $sum: "$0500.PassTraffic"
        },
        "PassTraffic|0501": {
            $sum: "$0501.PassTraffic"
        },
        "PassTraffic|0502": {
            $sum: "$0502.PassTraffic"
        },
        "PassTraffic|0503": {
            $sum: "$0503.PassTraffic"
        },
        "PassTraffic|0504": {
            $sum: "$0504.PassTraffic"
        },
        "PassTraffic|0505": {
            $sum: "$0505.PassTraffic"
        },
        "PassTraffic|0506": {
            $sum: "$0506.PassTraffic"
        },
        "PassTraffic|0507": {
            $sum: "$0507.PassTraffic"
        },
        "PassTraffic|0508": {
            $sum: "$0508.PassTraffic"
        },
        "PassTraffic|0509": {
            $sum: "$0509.PassTraffic"
        },
        "PassTraffic|0510": {
            $sum: "$0510.PassTraffic"
        },
        "PassTraffic|0511": {
            $sum: "$0511.PassTraffic"
        },
        "PassTraffic|0512": {
            $sum: "$0512.PassTraffic"
        },
        "PassTraffic|0513": {
            $sum: "$0513.PassTraffic"
        },
        "PassTraffic|0514": {
            $sum: "$0514.PassTraffic"
        },
        "PassTraffic|0515": {
            $sum: "$0515.PassTraffic"
        },
        "PassTraffic|0516": {
            $sum: "$0516.PassTraffic"
        },
        "PassTraffic|0517": {
            $sum: "$0517.PassTraffic"
        },
        "PassTraffic|0518": {
            $sum: "$0518.PassTraffic"
        },
        "PassTraffic|0519": {
            $sum: "$0519.PassTraffic"
        },
        "PassTraffic|0520": {
            $sum: "$0520.PassTraffic"
        },
        "PassTraffic|0521": {
            $sum: "$0521.PassTraffic"
        },
        "PassTraffic|0522": {
            $sum: "$0522.PassTraffic"
        },
        "PassTraffic|0523": {
            $sum: "$0523.PassTraffic"
        },
        "PassTraffic|0524": {
            $sum: "$0524.PassTraffic"
        },
        "PassTraffic|0525": {
            $sum: "$0525.PassTraffic"
        },
        "PassTraffic|0526": {
            $sum: "$0526.PassTraffic"
        },
        "PassTraffic|0527": {
            $sum: "$0527.PassTraffic"
        },
        "PassTraffic|0528": {
            $sum: "$0528.PassTraffic"
        },
        "PassTraffic|0529": {
            $sum: "$0529.PassTraffic"
        },
        "PassTraffic|0530": {
            $sum: "$0530.PassTraffic"
        },
        "PassTraffic|0531": {
            $sum: "$0531.PassTraffic"
        },
        "PassTraffic|0532": {
            $sum: "$0532.PassTraffic"
        },
        "PassTraffic|0533": {
            $sum: "$0533.PassTraffic"
        },
        "PassTraffic|0534": {
            $sum: "$0534.PassTraffic"
        },
        "PassTraffic|0535": {
            $sum: "$0535.PassTraffic"
        },
        "PassTraffic|0536": {
            $sum: "$0536.PassTraffic"
        },
        "PassTraffic|0537": {
            $sum: "$0537.PassTraffic"
        },
        "PassTraffic|0538": {
            $sum: "$0538.PassTraffic"
        },
        "PassTraffic|0539": {
            $sum: "$0539.PassTraffic"
        },
        "PassTraffic|0540": {
            $sum: "$0540.PassTraffic"
        },
        "PassTraffic|0541": {
            $sum: "$0541.PassTraffic"
        },
        "PassTraffic|0542": {
            $sum: "$0542.PassTraffic"
        },
        "PassTraffic|0543": {
            $sum: "$0543.PassTraffic"
        },
        "PassTraffic|0544": {
            $sum: "$0544.PassTraffic"
        },
        "PassTraffic|0545": {
            $sum: "$0545.PassTraffic"
        },
        "PassTraffic|0546": {
            $sum: "$0546.PassTraffic"
        },
        "PassTraffic|0547": {
            $sum: "$0547.PassTraffic"
        },
        "PassTraffic|0548": {
            $sum: "$0548.PassTraffic"
        },
        "PassTraffic|0549": {
            $sum: "$0549.PassTraffic"
        },
        "PassTraffic|0550": {
            $sum: "$0550.PassTraffic"
        },
        "PassTraffic|0551": {
            $sum: "$0551.PassTraffic"
        },
        "PassTraffic|0552": {
            $sum: "$0552.PassTraffic"
        },
        "PassTraffic|0553": {
            $sum: "$0553.PassTraffic"
        },
        "PassTraffic|0554": {
            $sum: "$0554.PassTraffic"
        },
        "PassTraffic|0555": {
            $sum: "$0555.PassTraffic"
        },
        "PassTraffic|0556": {
            $sum: "$0556.PassTraffic"
        },
        "PassTraffic|0557": {
            $sum: "$0557.PassTraffic"
        },
        "PassTraffic|0558": {
            $sum: "$0558.PassTraffic"
        },
        "PassTraffic|0559": {
            $sum: "$0559.PassTraffic"
        },
        "PassTraffic|0600": {
            $sum: "$0600.PassTraffic"
        },
        "PassTraffic|0601": {
            $sum: "$0601.PassTraffic"
        },
        "PassTraffic|0602": {
            $sum: "$0602.PassTraffic"
        },
        "PassTraffic|0603": {
            $sum: "$0603.PassTraffic"
        },
        "PassTraffic|0604": {
            $sum: "$0604.PassTraffic"
        },
        "PassTraffic|0605": {
            $sum: "$0605.PassTraffic"
        },
        "PassTraffic|0606": {
            $sum: "$0606.PassTraffic"
        },
        "PassTraffic|0607": {
            $sum: "$0607.PassTraffic"
        },
        "PassTraffic|0608": {
            $sum: "$0608.PassTraffic"
        },
        "PassTraffic|0609": {
            $sum: "$0609.PassTraffic"
        },
        "PassTraffic|0610": {
            $sum: "$0610.PassTraffic"
        },
        "PassTraffic|0611": {
            $sum: "$0611.PassTraffic"
        },
        "PassTraffic|0612": {
            $sum: "$0612.PassTraffic"
        },
        "PassTraffic|0613": {
            $sum: "$0613.PassTraffic"
        },
        "PassTraffic|0614": {
            $sum: "$0614.PassTraffic"
        },
        "PassTraffic|0615": {
            $sum: "$0615.PassTraffic"
        },
        "PassTraffic|0616": {
            $sum: "$0616.PassTraffic"
        },
        "PassTraffic|0617": {
            $sum: "$0617.PassTraffic"
        },
        "PassTraffic|0618": {
            $sum: "$0618.PassTraffic"
        },
        "PassTraffic|0619": {
            $sum: "$0619.PassTraffic"
        },
        "PassTraffic|0620": {
            $sum: "$0620.PassTraffic"
        },
        "PassTraffic|0621": {
            $sum: "$0621.PassTraffic"
        },
        "PassTraffic|0622": {
            $sum: "$0622.PassTraffic"
        },
        "PassTraffic|0623": {
            $sum: "$0623.PassTraffic"
        },
        "PassTraffic|0624": {
            $sum: "$0624.PassTraffic"
        },
        "PassTraffic|0625": {
            $sum: "$0625.PassTraffic"
        },
        "PassTraffic|0626": {
            $sum: "$0626.PassTraffic"
        },
        "PassTraffic|0627": {
            $sum: "$0627.PassTraffic"
        },
        "PassTraffic|0628": {
            $sum: "$0628.PassTraffic"
        },
        "PassTraffic|0629": {
            $sum: "$0629.PassTraffic"
        },
        "PassTraffic|0630": {
            $sum: "$0630.PassTraffic"
        },
        "PassTraffic|0631": {
            $sum: "$0631.PassTraffic"
        },
        "PassTraffic|0632": {
            $sum: "$0632.PassTraffic"
        },
        "PassTraffic|0633": {
            $sum: "$0633.PassTraffic"
        },
        "PassTraffic|0634": {
            $sum: "$0634.PassTraffic"
        },
        "PassTraffic|0635": {
            $sum: "$0635.PassTraffic"
        },
        "PassTraffic|0636": {
            $sum: "$0636.PassTraffic"
        },
        "PassTraffic|0637": {
            $sum: "$0637.PassTraffic"
        },
        "PassTraffic|0638": {
            $sum: "$0638.PassTraffic"
        },
        "PassTraffic|0639": {
            $sum: "$0639.PassTraffic"
        },
        "PassTraffic|0640": {
            $sum: "$0640.PassTraffic"
        },
        "PassTraffic|0641": {
            $sum: "$0641.PassTraffic"
        },
        "PassTraffic|0642": {
            $sum: "$0642.PassTraffic"
        },
        "PassTraffic|0643": {
            $sum: "$0643.PassTraffic"
        },
        "PassTraffic|0644": {
            $sum: "$0644.PassTraffic"
        },
        "PassTraffic|0645": {
            $sum: "$0645.PassTraffic"
        },
        "PassTraffic|0646": {
            $sum: "$0646.PassTraffic"
        },
        "PassTraffic|0647": {
            $sum: "$0647.PassTraffic"
        },
        "PassTraffic|0648": {
            $sum: "$0648.PassTraffic"
        },
        "PassTraffic|0649": {
            $sum: "$0649.PassTraffic"
        },
        "PassTraffic|0650": {
            $sum: "$0650.PassTraffic"
        },
        "PassTraffic|0651": {
            $sum: "$0651.PassTraffic"
        },
        "PassTraffic|0652": {
            $sum: "$0652.PassTraffic"
        },
        "PassTraffic|0653": {
            $sum: "$0653.PassTraffic"
        },
        "PassTraffic|0654": {
            $sum: "$0654.PassTraffic"
        },
        "PassTraffic|0655": {
            $sum: "$0655.PassTraffic"
        },
        "PassTraffic|0656": {
            $sum: "$0656.PassTraffic"
        },
        "PassTraffic|0657": {
            $sum: "$0657.PassTraffic"
        },
        "PassTraffic|0658": {
            $sum: "$0658.PassTraffic"
        },
        "PassTraffic|0659": {
            $sum: "$0659.PassTraffic"
        },
        "PassTraffic|0700": {
            $sum: "$0700.PassTraffic"
        },
        "PassTraffic|0701": {
            $sum: "$0701.PassTraffic"
        },
        "PassTraffic|0702": {
            $sum: "$0702.PassTraffic"
        },
        "PassTraffic|0703": {
            $sum: "$0703.PassTraffic"
        },
        "PassTraffic|0704": {
            $sum: "$0704.PassTraffic"
        },
        "PassTraffic|0705": {
            $sum: "$0705.PassTraffic"
        },
        "PassTraffic|0706": {
            $sum: "$0706.PassTraffic"
        },
        "PassTraffic|0707": {
            $sum: "$0707.PassTraffic"
        },
        "PassTraffic|0708": {
            $sum: "$0708.PassTraffic"
        },
        "PassTraffic|0709": {
            $sum: "$0709.PassTraffic"
        },
        "PassTraffic|0710": {
            $sum: "$0710.PassTraffic"
        },
        "PassTraffic|0711": {
            $sum: "$0711.PassTraffic"
        },
        "PassTraffic|0712": {
            $sum: "$0712.PassTraffic"
        },
        "PassTraffic|0713": {
            $sum: "$0713.PassTraffic"
        },
        "PassTraffic|0714": {
            $sum: "$0714.PassTraffic"
        },
        "PassTraffic|0715": {
            $sum: "$0715.PassTraffic"
        },
        "PassTraffic|0716": {
            $sum: "$0716.PassTraffic"
        },
        "PassTraffic|0717": {
            $sum: "$0717.PassTraffic"
        },
        "PassTraffic|0718": {
            $sum: "$0718.PassTraffic"
        },
        "PassTraffic|0719": {
            $sum: "$0719.PassTraffic"
        },
        "PassTraffic|0720": {
            $sum: "$0720.PassTraffic"
        },
        "PassTraffic|0721": {
            $sum: "$0721.PassTraffic"
        },
        "PassTraffic|0722": {
            $sum: "$0722.PassTraffic"
        },
        "PassTraffic|0723": {
            $sum: "$0723.PassTraffic"
        },
        "PassTraffic|0724": {
            $sum: "$0724.PassTraffic"
        },
        "PassTraffic|0725": {
            $sum: "$0725.PassTraffic"
        },
        "PassTraffic|0726": {
            $sum: "$0726.PassTraffic"
        },
        "PassTraffic|0727": {
            $sum: "$0727.PassTraffic"
        },
        "PassTraffic|0728": {
            $sum: "$0728.PassTraffic"
        },
        "PassTraffic|0729": {
            $sum: "$0729.PassTraffic"
        },
        "PassTraffic|0730": {
            $sum: "$0730.PassTraffic"
        },
        "PassTraffic|0731": {
            $sum: "$0731.PassTraffic"
        },
        "PassTraffic|0732": {
            $sum: "$0732.PassTraffic"
        },
        "PassTraffic|0733": {
            $sum: "$0733.PassTraffic"
        },
        "PassTraffic|0734": {
            $sum: "$0734.PassTraffic"
        },
        "PassTraffic|0735": {
            $sum: "$0735.PassTraffic"
        },
        "PassTraffic|0736": {
            $sum: "$0736.PassTraffic"
        },
        "PassTraffic|0737": {
            $sum: "$0737.PassTraffic"
        },
        "PassTraffic|0738": {
            $sum: "$0738.PassTraffic"
        },
        "PassTraffic|0739": {
            $sum: "$0739.PassTraffic"
        },
        "PassTraffic|0740": {
            $sum: "$0740.PassTraffic"
        },
        "PassTraffic|0741": {
            $sum: "$0741.PassTraffic"
        },
        "PassTraffic|0742": {
            $sum: "$0742.PassTraffic"
        },
        "PassTraffic|0743": {
            $sum: "$0743.PassTraffic"
        },
        "PassTraffic|0744": {
            $sum: "$0744.PassTraffic"
        },
        "PassTraffic|0745": {
            $sum: "$0745.PassTraffic"
        },
        "PassTraffic|0746": {
            $sum: "$0746.PassTraffic"
        },
        "PassTraffic|0747": {
            $sum: "$0747.PassTraffic"
        },
        "PassTraffic|0748": {
            $sum: "$0748.PassTraffic"
        },
        "PassTraffic|0749": {
            $sum: "$0749.PassTraffic"
        },
        "PassTraffic|0750": {
            $sum: "$0750.PassTraffic"
        },
        "PassTraffic|0751": {
            $sum: "$0751.PassTraffic"
        },
        "PassTraffic|0752": {
            $sum: "$0752.PassTraffic"
        },
        "PassTraffic|0753": {
            $sum: "$0753.PassTraffic"
        },
        "PassTraffic|0754": {
            $sum: "$0754.PassTraffic"
        },
        "PassTraffic|0755": {
            $sum: "$0755.PassTraffic"
        },
        "PassTraffic|0756": {
            $sum: "$0756.PassTraffic"
        },
        "PassTraffic|0757": {
            $sum: "$0757.PassTraffic"
        },
        "PassTraffic|0758": {
            $sum: "$0758.PassTraffic"
        },
        "PassTraffic|0759": {
            $sum: "$0759.PassTraffic"
        },
        "PassTraffic|0800": {
            $sum: "$0800.PassTraffic"
        },
        "PassTraffic|0801": {
            $sum: "$0801.PassTraffic"
        },
        "PassTraffic|0802": {
            $sum: "$0802.PassTraffic"
        },
        "PassTraffic|0803": {
            $sum: "$0803.PassTraffic"
        },
        "PassTraffic|0804": {
            $sum: "$0804.PassTraffic"
        },
        "PassTraffic|0805": {
            $sum: "$0805.PassTraffic"
        },
        "PassTraffic|0806": {
            $sum: "$0806.PassTraffic"
        },
        "PassTraffic|0807": {
            $sum: "$0807.PassTraffic"
        },
        "PassTraffic|0808": {
            $sum: "$0808.PassTraffic"
        },
        "PassTraffic|0809": {
            $sum: "$0809.PassTraffic"
        },
        "PassTraffic|0810": {
            $sum: "$0810.PassTraffic"
        },
        "PassTraffic|0811": {
            $sum: "$0811.PassTraffic"
        },
        "PassTraffic|0812": {
            $sum: "$0812.PassTraffic"
        },
        "PassTraffic|0813": {
            $sum: "$0813.PassTraffic"
        },
        "PassTraffic|0814": {
            $sum: "$0814.PassTraffic"
        },
        "PassTraffic|0815": {
            $sum: "$0815.PassTraffic"
        },
        "PassTraffic|0816": {
            $sum: "$0816.PassTraffic"
        },
        "PassTraffic|0817": {
            $sum: "$0817.PassTraffic"
        },
        "PassTraffic|0818": {
            $sum: "$0818.PassTraffic"
        },
        "PassTraffic|0819": {
            $sum: "$0819.PassTraffic"
        },
        "PassTraffic|0820": {
            $sum: "$0820.PassTraffic"
        },
        "PassTraffic|0821": {
            $sum: "$0821.PassTraffic"
        },
        "PassTraffic|0822": {
            $sum: "$0822.PassTraffic"
        },
        "PassTraffic|0823": {
            $sum: "$0823.PassTraffic"
        },
        "PassTraffic|0824": {
            $sum: "$0824.PassTraffic"
        },
        "PassTraffic|0825": {
            $sum: "$0825.PassTraffic"
        },
        "PassTraffic|0826": {
            $sum: "$0826.PassTraffic"
        },
        "PassTraffic|0827": {
            $sum: "$0827.PassTraffic"
        },
        "PassTraffic|0828": {
            $sum: "$0828.PassTraffic"
        },
        "PassTraffic|0829": {
            $sum: "$0829.PassTraffic"
        },
        "PassTraffic|0830": {
            $sum: "$0830.PassTraffic"
        },
        "PassTraffic|0831": {
            $sum: "$0831.PassTraffic"
        },
        "PassTraffic|0832": {
            $sum: "$0832.PassTraffic"
        },
        "PassTraffic|0833": {
            $sum: "$0833.PassTraffic"
        },
        "PassTraffic|0834": {
            $sum: "$0834.PassTraffic"
        },
        "PassTraffic|0835": {
            $sum: "$0835.PassTraffic"
        },
        "PassTraffic|0836": {
            $sum: "$0836.PassTraffic"
        },
        "PassTraffic|0837": {
            $sum: "$0837.PassTraffic"
        },
        "PassTraffic|0838": {
            $sum: "$0838.PassTraffic"
        },
        "PassTraffic|0839": {
            $sum: "$0839.PassTraffic"
        },
        "PassTraffic|0840": {
            $sum: "$0840.PassTraffic"
        },
        "PassTraffic|0841": {
            $sum: "$0841.PassTraffic"
        },
        "PassTraffic|0842": {
            $sum: "$0842.PassTraffic"
        },
        "PassTraffic|0843": {
            $sum: "$0843.PassTraffic"
        },
        "PassTraffic|0844": {
            $sum: "$0844.PassTraffic"
        },
        "PassTraffic|0845": {
            $sum: "$0845.PassTraffic"
        },
        "PassTraffic|0846": {
            $sum: "$0846.PassTraffic"
        },
        "PassTraffic|0847": {
            $sum: "$0847.PassTraffic"
        },
        "PassTraffic|0848": {
            $sum: "$0848.PassTraffic"
        },
        "PassTraffic|0849": {
            $sum: "$0849.PassTraffic"
        },
        "PassTraffic|0850": {
            $sum: "$0850.PassTraffic"
        },
        "PassTraffic|0851": {
            $sum: "$0851.PassTraffic"
        },
        "PassTraffic|0852": {
            $sum: "$0852.PassTraffic"
        },
        "PassTraffic|0853": {
            $sum: "$0853.PassTraffic"
        },
        "PassTraffic|0854": {
            $sum: "$0854.PassTraffic"
        },
        "PassTraffic|0855": {
            $sum: "$0855.PassTraffic"
        },
        "PassTraffic|0856": {
            $sum: "$0856.PassTraffic"
        },
        "PassTraffic|0857": {
            $sum: "$0857.PassTraffic"
        },
        "PassTraffic|0858": {
            $sum: "$0858.PassTraffic"
        },
        "PassTraffic|0859": {
            $sum: "$0859.PassTraffic"
        },
        "PassTraffic|0900": {
            $sum: "$0900.PassTraffic"
        },
        "PassTraffic|0901": {
            $sum: "$0901.PassTraffic"
        },
        "PassTraffic|0902": {
            $sum: "$0902.PassTraffic"
        },
        "PassTraffic|0903": {
            $sum: "$0903.PassTraffic"
        },
        "PassTraffic|0904": {
            $sum: "$0904.PassTraffic"
        },
        "PassTraffic|0905": {
            $sum: "$0905.PassTraffic"
        },
        "PassTraffic|0906": {
            $sum: "$0906.PassTraffic"
        },
        "PassTraffic|0907": {
            $sum: "$0907.PassTraffic"
        },
        "PassTraffic|0908": {
            $sum: "$0908.PassTraffic"
        },
        "PassTraffic|0909": {
            $sum: "$0909.PassTraffic"
        },
        "PassTraffic|0910": {
            $sum: "$0910.PassTraffic"
        },
        "PassTraffic|0911": {
            $sum: "$0911.PassTraffic"
        },
        "PassTraffic|0912": {
            $sum: "$0912.PassTraffic"
        },
        "PassTraffic|0913": {
            $sum: "$0913.PassTraffic"
        },
        "PassTraffic|0914": {
            $sum: "$0914.PassTraffic"
        },
        "PassTraffic|0915": {
            $sum: "$0915.PassTraffic"
        },
        "PassTraffic|0916": {
            $sum: "$0916.PassTraffic"
        },
        "PassTraffic|0917": {
            $sum: "$0917.PassTraffic"
        },
        "PassTraffic|0918": {
            $sum: "$0918.PassTraffic"
        },
        "PassTraffic|0919": {
            $sum: "$0919.PassTraffic"
        },
        "PassTraffic|0920": {
            $sum: "$0920.PassTraffic"
        },
        "PassTraffic|0921": {
            $sum: "$0921.PassTraffic"
        },
        "PassTraffic|0922": {
            $sum: "$0922.PassTraffic"
        },
        "PassTraffic|0923": {
            $sum: "$0923.PassTraffic"
        },
        "PassTraffic|0924": {
            $sum: "$0924.PassTraffic"
        },
        "PassTraffic|0925": {
            $sum: "$0925.PassTraffic"
        },
        "PassTraffic|0926": {
            $sum: "$0926.PassTraffic"
        },
        "PassTraffic|0927": {
            $sum: "$0927.PassTraffic"
        },
        "PassTraffic|0928": {
            $sum: "$0928.PassTraffic"
        },
        "PassTraffic|0929": {
            $sum: "$0929.PassTraffic"
        },
        "PassTraffic|0930": {
            $sum: "$0930.PassTraffic"
        },
        "PassTraffic|0931": {
            $sum: "$0931.PassTraffic"
        },
        "PassTraffic|0932": {
            $sum: "$0932.PassTraffic"
        },
        "PassTraffic|0933": {
            $sum: "$0933.PassTraffic"
        },
        "PassTraffic|0934": {
            $sum: "$0934.PassTraffic"
        },
        "PassTraffic|0935": {
            $sum: "$0935.PassTraffic"
        },
        "PassTraffic|0936": {
            $sum: "$0936.PassTraffic"
        },
        "PassTraffic|0937": {
            $sum: "$0937.PassTraffic"
        },
        "PassTraffic|0938": {
            $sum: "$0938.PassTraffic"
        },
        "PassTraffic|0939": {
            $sum: "$0939.PassTraffic"
        },
        "PassTraffic|0940": {
            $sum: "$0940.PassTraffic"
        },
        "PassTraffic|0941": {
            $sum: "$0941.PassTraffic"
        },
        "PassTraffic|0942": {
            $sum: "$0942.PassTraffic"
        },
        "PassTraffic|0943": {
            $sum: "$0943.PassTraffic"
        },
        "PassTraffic|0944": {
            $sum: "$0944.PassTraffic"
        },
        "PassTraffic|0945": {
            $sum: "$0945.PassTraffic"
        },
        "PassTraffic|0946": {
            $sum: "$0946.PassTraffic"
        },
        "PassTraffic|0947": {
            $sum: "$0947.PassTraffic"
        },
        "PassTraffic|0948": {
            $sum: "$0948.PassTraffic"
        },
        "PassTraffic|0949": {
            $sum: "$0949.PassTraffic"
        },
        "PassTraffic|0950": {
            $sum: "$0950.PassTraffic"
        },
        "PassTraffic|0951": {
            $sum: "$0951.PassTraffic"
        },
        "PassTraffic|0952": {
            $sum: "$0952.PassTraffic"
        },
        "PassTraffic|0953": {
            $sum: "$0953.PassTraffic"
        },
        "PassTraffic|0954": {
            $sum: "$0954.PassTraffic"
        },
        "PassTraffic|0955": {
            $sum: "$0955.PassTraffic"
        },
        "PassTraffic|0956": {
            $sum: "$0956.PassTraffic"
        },
        "PassTraffic|0957": {
            $sum: "$0957.PassTraffic"
        },
        "PassTraffic|0958": {
            $sum: "$0958.PassTraffic"
        },
        "PassTraffic|0959": {
            $sum: "$0959.PassTraffic"
        },
        "PassTraffic|1000": {
            $sum: "$1000.PassTraffic"
        },
        "PassTraffic|1001": {
            $sum: "$1001.PassTraffic"
        },
        "PassTraffic|1002": {
            $sum: "$1002.PassTraffic"
        },
        "PassTraffic|1003": {
            $sum: "$1003.PassTraffic"
        },
        "PassTraffic|1004": {
            $sum: "$1004.PassTraffic"
        },
        "PassTraffic|1005": {
            $sum: "$1005.PassTraffic"
        },
        "PassTraffic|1006": {
            $sum: "$1006.PassTraffic"
        },
        "PassTraffic|1007": {
            $sum: "$1007.PassTraffic"
        },
        "PassTraffic|1008": {
            $sum: "$1008.PassTraffic"
        },
        "PassTraffic|1009": {
            $sum: "$1009.PassTraffic"
        },
        "PassTraffic|1010": {
            $sum: "$1010.PassTraffic"
        },
        "PassTraffic|1011": {
            $sum: "$1011.PassTraffic"
        },
        "PassTraffic|1012": {
            $sum: "$1012.PassTraffic"
        },
        "PassTraffic|1013": {
            $sum: "$1013.PassTraffic"
        },
        "PassTraffic|1014": {
            $sum: "$1014.PassTraffic"
        },
        "PassTraffic|1015": {
            $sum: "$1015.PassTraffic"
        },
        "PassTraffic|1016": {
            $sum: "$1016.PassTraffic"
        },
        "PassTraffic|1017": {
            $sum: "$1017.PassTraffic"
        },
        "PassTraffic|1018": {
            $sum: "$1018.PassTraffic"
        },
        "PassTraffic|1019": {
            $sum: "$1019.PassTraffic"
        },
        "PassTraffic|1020": {
            $sum: "$1020.PassTraffic"
        },
        "PassTraffic|1021": {
            $sum: "$1021.PassTraffic"
        },
        "PassTraffic|1022": {
            $sum: "$1022.PassTraffic"
        },
        "PassTraffic|1023": {
            $sum: "$1023.PassTraffic"
        },
        "PassTraffic|1024": {
            $sum: "$1024.PassTraffic"
        },
        "PassTraffic|1025": {
            $sum: "$1025.PassTraffic"
        },
        "PassTraffic|1026": {
            $sum: "$1026.PassTraffic"
        },
        "PassTraffic|1027": {
            $sum: "$1027.PassTraffic"
        },
        "PassTraffic|1028": {
            $sum: "$1028.PassTraffic"
        },
        "PassTraffic|1029": {
            $sum: "$1029.PassTraffic"
        },
        "PassTraffic|1030": {
            $sum: "$1030.PassTraffic"
        },
        "PassTraffic|1031": {
            $sum: "$1031.PassTraffic"
        },
        "PassTraffic|1032": {
            $sum: "$1032.PassTraffic"
        },
        "PassTraffic|1033": {
            $sum: "$1033.PassTraffic"
        },
        "PassTraffic|1034": {
            $sum: "$1034.PassTraffic"
        },
        "PassTraffic|1035": {
            $sum: "$1035.PassTraffic"
        },
        "PassTraffic|1036": {
            $sum: "$1036.PassTraffic"
        },
        "PassTraffic|1037": {
            $sum: "$1037.PassTraffic"
        },
        "PassTraffic|1038": {
            $sum: "$1038.PassTraffic"
        },
        "PassTraffic|1039": {
            $sum: "$1039.PassTraffic"
        },
        "PassTraffic|1040": {
            $sum: "$1040.PassTraffic"
        },
        "PassTraffic|1041": {
            $sum: "$1041.PassTraffic"
        },
        "PassTraffic|1042": {
            $sum: "$1042.PassTraffic"
        },
        "PassTraffic|1043": {
            $sum: "$1043.PassTraffic"
        },
        "PassTraffic|1044": {
            $sum: "$1044.PassTraffic"
        },
        "PassTraffic|1045": {
            $sum: "$1045.PassTraffic"
        },
        "PassTraffic|1046": {
            $sum: "$1046.PassTraffic"
        },
        "PassTraffic|1047": {
            $sum: "$1047.PassTraffic"
        },
        "PassTraffic|1048": {
            $sum: "$1048.PassTraffic"
        },
        "PassTraffic|1049": {
            $sum: "$1049.PassTraffic"
        },
        "PassTraffic|1050": {
            $sum: "$1050.PassTraffic"
        },
        "PassTraffic|1051": {
            $sum: "$1051.PassTraffic"
        },
        "PassTraffic|1052": {
            $sum: "$1052.PassTraffic"
        },
        "PassTraffic|1053": {
            $sum: "$1053.PassTraffic"
        },
        "PassTraffic|1054": {
            $sum: "$1054.PassTraffic"
        },
        "PassTraffic|1055": {
            $sum: "$1055.PassTraffic"
        },
        "PassTraffic|1056": {
            $sum: "$1056.PassTraffic"
        },
        "PassTraffic|1057": {
            $sum: "$1057.PassTraffic"
        },
        "PassTraffic|1058": {
            $sum: "$1058.PassTraffic"
        },
        "PassTraffic|1059": {
            $sum: "$1059.PassTraffic"
        },
        "PassTraffic|1100": {
            $sum: "$1100.PassTraffic"
        },
        "PassTraffic|1101": {
            $sum: "$1101.PassTraffic"
        },
        "PassTraffic|1102": {
            $sum: "$1102.PassTraffic"
        },
        "PassTraffic|1103": {
            $sum: "$1103.PassTraffic"
        },
        "PassTraffic|1104": {
            $sum: "$1104.PassTraffic"
        },
        "PassTraffic|1105": {
            $sum: "$1105.PassTraffic"
        },
        "PassTraffic|1106": {
            $sum: "$1106.PassTraffic"
        },
        "PassTraffic|1107": {
            $sum: "$1107.PassTraffic"
        },
        "PassTraffic|1108": {
            $sum: "$1108.PassTraffic"
        },
        "PassTraffic|1109": {
            $sum: "$1109.PassTraffic"
        },
        "PassTraffic|1110": {
            $sum: "$1110.PassTraffic"
        },
        "PassTraffic|1111": {
            $sum: "$1111.PassTraffic"
        },
        "PassTraffic|1112": {
            $sum: "$1112.PassTraffic"
        },
        "PassTraffic|1113": {
            $sum: "$1113.PassTraffic"
        },
        "PassTraffic|1114": {
            $sum: "$1114.PassTraffic"
        },
        "PassTraffic|1115": {
            $sum: "$1115.PassTraffic"
        },
        "PassTraffic|1116": {
            $sum: "$1116.PassTraffic"
        },
        "PassTraffic|1117": {
            $sum: "$1117.PassTraffic"
        },
        "PassTraffic|1118": {
            $sum: "$1118.PassTraffic"
        },
        "PassTraffic|1119": {
            $sum: "$1119.PassTraffic"
        },
        "PassTraffic|1120": {
            $sum: "$1120.PassTraffic"
        },
        "PassTraffic|1121": {
            $sum: "$1121.PassTraffic"
        },
        "PassTraffic|1122": {
            $sum: "$1122.PassTraffic"
        },
        "PassTraffic|1123": {
            $sum: "$1123.PassTraffic"
        },
        "PassTraffic|1124": {
            $sum: "$1124.PassTraffic"
        },
        "PassTraffic|1125": {
            $sum: "$1125.PassTraffic"
        },
        "PassTraffic|1126": {
            $sum: "$1126.PassTraffic"
        },
        "PassTraffic|1127": {
            $sum: "$1127.PassTraffic"
        },
        "PassTraffic|1128": {
            $sum: "$1128.PassTraffic"
        },
        "PassTraffic|1129": {
            $sum: "$1129.PassTraffic"
        },
        "PassTraffic|1130": {
            $sum: "$1130.PassTraffic"
        },
        "PassTraffic|1131": {
            $sum: "$1131.PassTraffic"
        },
        "PassTraffic|1132": {
            $sum: "$1132.PassTraffic"
        },
        "PassTraffic|1133": {
            $sum: "$1133.PassTraffic"
        },
        "PassTraffic|1134": {
            $sum: "$1134.PassTraffic"
        },
        "PassTraffic|1135": {
            $sum: "$1135.PassTraffic"
        },
        "PassTraffic|1136": {
            $sum: "$1136.PassTraffic"
        },
        "PassTraffic|1137": {
            $sum: "$1137.PassTraffic"
        },
        "PassTraffic|1138": {
            $sum: "$1138.PassTraffic"
        },
        "PassTraffic|1139": {
            $sum: "$1139.PassTraffic"
        },
        "PassTraffic|1140": {
            $sum: "$1140.PassTraffic"
        },
        "PassTraffic|1141": {
            $sum: "$1141.PassTraffic"
        },
        "PassTraffic|1142": {
            $sum: "$1142.PassTraffic"
        },
        "PassTraffic|1143": {
            $sum: "$1143.PassTraffic"
        },
        "PassTraffic|1144": {
            $sum: "$1144.PassTraffic"
        },
        "PassTraffic|1145": {
            $sum: "$1145.PassTraffic"
        },
        "PassTraffic|1146": {
            $sum: "$1146.PassTraffic"
        },
        "PassTraffic|1147": {
            $sum: "$1147.PassTraffic"
        },
        "PassTraffic|1148": {
            $sum: "$1148.PassTraffic"
        },
        "PassTraffic|1149": {
            $sum: "$1149.PassTraffic"
        },
        "PassTraffic|1150": {
            $sum: "$1150.PassTraffic"
        },
        "PassTraffic|1151": {
            $sum: "$1151.PassTraffic"
        },
        "PassTraffic|1152": {
            $sum: "$1152.PassTraffic"
        },
        "PassTraffic|1153": {
            $sum: "$1153.PassTraffic"
        },
        "PassTraffic|1154": {
            $sum: "$1154.PassTraffic"
        },
        "PassTraffic|1155": {
            $sum: "$1155.PassTraffic"
        },
        "PassTraffic|1156": {
            $sum: "$1156.PassTraffic"
        },
        "PassTraffic|1157": {
            $sum: "$1157.PassTraffic"
        },
        "PassTraffic|1158": {
            $sum: "$1158.PassTraffic"
        },
        "PassTraffic|1159": {
            $sum: "$1159.PassTraffic"
        },
        "PassTraffic|1200": {
            $sum: "$1200.PassTraffic"
        },
        "PassTraffic|1201": {
            $sum: "$1201.PassTraffic"
        },
        "PassTraffic|1202": {
            $sum: "$1202.PassTraffic"
        },
        "PassTraffic|1203": {
            $sum: "$1203.PassTraffic"
        },
        "PassTraffic|1204": {
            $sum: "$1204.PassTraffic"
        },
        "PassTraffic|1205": {
            $sum: "$1205.PassTraffic"
        },
        "PassTraffic|1206": {
            $sum: "$1206.PassTraffic"
        },
        "PassTraffic|1207": {
            $sum: "$1207.PassTraffic"
        },
        "PassTraffic|1208": {
            $sum: "$1208.PassTraffic"
        },
        "PassTraffic|1209": {
            $sum: "$1209.PassTraffic"
        },
        "PassTraffic|1210": {
            $sum: "$1210.PassTraffic"
        },
        "PassTraffic|1211": {
            $sum: "$1211.PassTraffic"
        },
        "PassTraffic|1212": {
            $sum: "$1212.PassTraffic"
        },
        "PassTraffic|1213": {
            $sum: "$1213.PassTraffic"
        },
        "PassTraffic|1214": {
            $sum: "$1214.PassTraffic"
        },
        "PassTraffic|1215": {
            $sum: "$1215.PassTraffic"
        },
        "PassTraffic|1216": {
            $sum: "$1216.PassTraffic"
        },
        "PassTraffic|1217": {
            $sum: "$1217.PassTraffic"
        },
        "PassTraffic|1218": {
            $sum: "$1218.PassTraffic"
        },
        "PassTraffic|1219": {
            $sum: "$1219.PassTraffic"
        },
        "PassTraffic|1220": {
            $sum: "$1220.PassTraffic"
        },
        "PassTraffic|1221": {
            $sum: "$1221.PassTraffic"
        },
        "PassTraffic|1222": {
            $sum: "$1222.PassTraffic"
        },
        "PassTraffic|1223": {
            $sum: "$1223.PassTraffic"
        },
        "PassTraffic|1224": {
            $sum: "$1224.PassTraffic"
        },
        "PassTraffic|1225": {
            $sum: "$1225.PassTraffic"
        },
        "PassTraffic|1226": {
            $sum: "$1226.PassTraffic"
        },
        "PassTraffic|1227": {
            $sum: "$1227.PassTraffic"
        },
        "PassTraffic|1228": {
            $sum: "$1228.PassTraffic"
        },
        "PassTraffic|1229": {
            $sum: "$1229.PassTraffic"
        },
        "PassTraffic|1230": {
            $sum: "$1230.PassTraffic"
        },
        "PassTraffic|1231": {
            $sum: "$1231.PassTraffic"
        },
        "PassTraffic|1232": {
            $sum: "$1232.PassTraffic"
        },
        "PassTraffic|1233": {
            $sum: "$1233.PassTraffic"
        },
        "PassTraffic|1234": {
            $sum: "$1234.PassTraffic"
        },
        "PassTraffic|1235": {
            $sum: "$1235.PassTraffic"
        },
        "PassTraffic|1236": {
            $sum: "$1236.PassTraffic"
        },
        "PassTraffic|1237": {
            $sum: "$1237.PassTraffic"
        },
        "PassTraffic|1238": {
            $sum: "$1238.PassTraffic"
        },
        "PassTraffic|1239": {
            $sum: "$1239.PassTraffic"
        },
        "PassTraffic|1240": {
            $sum: "$1240.PassTraffic"
        },
        "PassTraffic|1241": {
            $sum: "$1241.PassTraffic"
        },
        "PassTraffic|1242": {
            $sum: "$1242.PassTraffic"
        },
        "PassTraffic|1243": {
            $sum: "$1243.PassTraffic"
        },
        "PassTraffic|1244": {
            $sum: "$1244.PassTraffic"
        },
        "PassTraffic|1245": {
            $sum: "$1245.PassTraffic"
        },
        "PassTraffic|1246": {
            $sum: "$1246.PassTraffic"
        },
        "PassTraffic|1247": {
            $sum: "$1247.PassTraffic"
        },
        "PassTraffic|1248": {
            $sum: "$1248.PassTraffic"
        },
        "PassTraffic|1249": {
            $sum: "$1249.PassTraffic"
        },
        "PassTraffic|1250": {
            $sum: "$1250.PassTraffic"
        },
        "PassTraffic|1251": {
            $sum: "$1251.PassTraffic"
        },
        "PassTraffic|1252": {
            $sum: "$1252.PassTraffic"
        },
        "PassTraffic|1253": {
            $sum: "$1253.PassTraffic"
        },
        "PassTraffic|1254": {
            $sum: "$1254.PassTraffic"
        },
        "PassTraffic|1255": {
            $sum: "$1255.PassTraffic"
        },
        "PassTraffic|1256": {
            $sum: "$1256.PassTraffic"
        },
        "PassTraffic|1257": {
            $sum: "$1257.PassTraffic"
        },
        "PassTraffic|1258": {
            $sum: "$1258.PassTraffic"
        },
        "PassTraffic|1259": {
            $sum: "$1259.PassTraffic"
        },
        "PassTraffic|1300": {
            $sum: "$1300.PassTraffic"
        },
        "PassTraffic|1301": {
            $sum: "$1301.PassTraffic"
        },
        "PassTraffic|1302": {
            $sum: "$1302.PassTraffic"
        },
        "PassTraffic|1303": {
            $sum: "$1303.PassTraffic"
        },
        "PassTraffic|1304": {
            $sum: "$1304.PassTraffic"
        },
        "PassTraffic|1305": {
            $sum: "$1305.PassTraffic"
        },
        "PassTraffic|1306": {
            $sum: "$1306.PassTraffic"
        },
        "PassTraffic|1307": {
            $sum: "$1307.PassTraffic"
        },
        "PassTraffic|1308": {
            $sum: "$1308.PassTraffic"
        },
        "PassTraffic|1309": {
            $sum: "$1309.PassTraffic"
        },
        "PassTraffic|1310": {
            $sum: "$1310.PassTraffic"
        },
        "PassTraffic|1311": {
            $sum: "$1311.PassTraffic"
        },
        "PassTraffic|1312": {
            $sum: "$1312.PassTraffic"
        },
        "PassTraffic|1313": {
            $sum: "$1313.PassTraffic"
        },
        "PassTraffic|1314": {
            $sum: "$1314.PassTraffic"
        },
        "PassTraffic|1315": {
            $sum: "$1315.PassTraffic"
        },
        "PassTraffic|1316": {
            $sum: "$1316.PassTraffic"
        },
        "PassTraffic|1317": {
            $sum: "$1317.PassTraffic"
        },
        "PassTraffic|1318": {
            $sum: "$1318.PassTraffic"
        },
        "PassTraffic|1319": {
            $sum: "$1319.PassTraffic"
        },
        "PassTraffic|1320": {
            $sum: "$1320.PassTraffic"
        },
        "PassTraffic|1321": {
            $sum: "$1321.PassTraffic"
        },
        "PassTraffic|1322": {
            $sum: "$1322.PassTraffic"
        },
        "PassTraffic|1323": {
            $sum: "$1323.PassTraffic"
        },
        "PassTraffic|1324": {
            $sum: "$1324.PassTraffic"
        },
        "PassTraffic|1325": {
            $sum: "$1325.PassTraffic"
        },
        "PassTraffic|1326": {
            $sum: "$1326.PassTraffic"
        },
        "PassTraffic|1327": {
            $sum: "$1327.PassTraffic"
        },
        "PassTraffic|1328": {
            $sum: "$1328.PassTraffic"
        },
        "PassTraffic|1329": {
            $sum: "$1329.PassTraffic"
        },
        "PassTraffic|1330": {
            $sum: "$1330.PassTraffic"
        },
        "PassTraffic|1331": {
            $sum: "$1331.PassTraffic"
        },
        "PassTraffic|1332": {
            $sum: "$1332.PassTraffic"
        },
        "PassTraffic|1333": {
            $sum: "$1333.PassTraffic"
        },
        "PassTraffic|1334": {
            $sum: "$1334.PassTraffic"
        },
        "PassTraffic|1335": {
            $sum: "$1335.PassTraffic"
        },
        "PassTraffic|1336": {
            $sum: "$1336.PassTraffic"
        },
        "PassTraffic|1337": {
            $sum: "$1337.PassTraffic"
        },
        "PassTraffic|1338": {
            $sum: "$1338.PassTraffic"
        },
        "PassTraffic|1339": {
            $sum: "$1339.PassTraffic"
        },
        "PassTraffic|1340": {
            $sum: "$1340.PassTraffic"
        },
        "PassTraffic|1341": {
            $sum: "$1341.PassTraffic"
        },
        "PassTraffic|1342": {
            $sum: "$1342.PassTraffic"
        },
        "PassTraffic|1343": {
            $sum: "$1343.PassTraffic"
        },
        "PassTraffic|1344": {
            $sum: "$1344.PassTraffic"
        },
        "PassTraffic|1345": {
            $sum: "$1345.PassTraffic"
        },
        "PassTraffic|1346": {
            $sum: "$1346.PassTraffic"
        },
        "PassTraffic|1347": {
            $sum: "$1347.PassTraffic"
        },
        "PassTraffic|1348": {
            $sum: "$1348.PassTraffic"
        },
        "PassTraffic|1349": {
            $sum: "$1349.PassTraffic"
        },
        "PassTraffic|1350": {
            $sum: "$1350.PassTraffic"
        },
        "PassTraffic|1351": {
            $sum: "$1351.PassTraffic"
        },
        "PassTraffic|1352": {
            $sum: "$1352.PassTraffic"
        },
        "PassTraffic|1353": {
            $sum: "$1353.PassTraffic"
        },
        "PassTraffic|1354": {
            $sum: "$1354.PassTraffic"
        },
        "PassTraffic|1355": {
            $sum: "$1355.PassTraffic"
        },
        "PassTraffic|1356": {
            $sum: "$1356.PassTraffic"
        },
        "PassTraffic|1357": {
            $sum: "$1357.PassTraffic"
        },
        "PassTraffic|1358": {
            $sum: "$1358.PassTraffic"
        },
        "PassTraffic|1359": {
            $sum: "$1359.PassTraffic"
        },
        "PassTraffic|1400": {
            $sum: "$1400.PassTraffic"
        },
        "PassTraffic|1401": {
            $sum: "$1401.PassTraffic"
        },
        "PassTraffic|1402": {
            $sum: "$1402.PassTraffic"
        },
        "PassTraffic|1403": {
            $sum: "$1403.PassTraffic"
        },
        "PassTraffic|1404": {
            $sum: "$1404.PassTraffic"
        },
        "PassTraffic|1405": {
            $sum: "$1405.PassTraffic"
        },
        "PassTraffic|1406": {
            $sum: "$1406.PassTraffic"
        },
        "PassTraffic|1407": {
            $sum: "$1407.PassTraffic"
        },
        "PassTraffic|1408": {
            $sum: "$1408.PassTraffic"
        },
        "PassTraffic|1409": {
            $sum: "$1409.PassTraffic"
        },
        "PassTraffic|1410": {
            $sum: "$1410.PassTraffic"
        },
        "PassTraffic|1411": {
            $sum: "$1411.PassTraffic"
        },
        "PassTraffic|1412": {
            $sum: "$1412.PassTraffic"
        },
        "PassTraffic|1413": {
            $sum: "$1413.PassTraffic"
        },
        "PassTraffic|1414": {
            $sum: "$1414.PassTraffic"
        },
        "PassTraffic|1415": {
            $sum: "$1415.PassTraffic"
        },
        "PassTraffic|1416": {
            $sum: "$1416.PassTraffic"
        },
        "PassTraffic|1417": {
            $sum: "$1417.PassTraffic"
        },
        "PassTraffic|1418": {
            $sum: "$1418.PassTraffic"
        },
        "PassTraffic|1419": {
            $sum: "$1419.PassTraffic"
        },
        "PassTraffic|1420": {
            $sum: "$1420.PassTraffic"
        },
        "PassTraffic|1421": {
            $sum: "$1421.PassTraffic"
        },
        "PassTraffic|1422": {
            $sum: "$1422.PassTraffic"
        },
        "PassTraffic|1423": {
            $sum: "$1423.PassTraffic"
        },
        "PassTraffic|1424": {
            $sum: "$1424.PassTraffic"
        },
        "PassTraffic|1425": {
            $sum: "$1425.PassTraffic"
        },
        "PassTraffic|1426": {
            $sum: "$1426.PassTraffic"
        },
        "PassTraffic|1427": {
            $sum: "$1427.PassTraffic"
        },
        "PassTraffic|1428": {
            $sum: "$1428.PassTraffic"
        },
        "PassTraffic|1429": {
            $sum: "$1429.PassTraffic"
        },
        "PassTraffic|1430": {
            $sum: "$1430.PassTraffic"
        },
        "PassTraffic|1431": {
            $sum: "$1431.PassTraffic"
        },
        "PassTraffic|1432": {
            $sum: "$1432.PassTraffic"
        },
        "PassTraffic|1433": {
            $sum: "$1433.PassTraffic"
        },
        "PassTraffic|1434": {
            $sum: "$1434.PassTraffic"
        },
        "PassTraffic|1435": {
            $sum: "$1435.PassTraffic"
        },
        "PassTraffic|1436": {
            $sum: "$1436.PassTraffic"
        },
        "PassTraffic|1437": {
            $sum: "$1437.PassTraffic"
        },
        "PassTraffic|1438": {
            $sum: "$1438.PassTraffic"
        },
        "PassTraffic|1439": {
            $sum: "$1439.PassTraffic"
        },
        "PassTraffic|1440": {
            $sum: "$1440.PassTraffic"
        },
        "PassTraffic|1441": {
            $sum: "$1441.PassTraffic"
        },
        "PassTraffic|1442": {
            $sum: "$1442.PassTraffic"
        },
        "PassTraffic|1443": {
            $sum: "$1443.PassTraffic"
        },
        "PassTraffic|1444": {
            $sum: "$1444.PassTraffic"
        },
        "PassTraffic|1445": {
            $sum: "$1445.PassTraffic"
        },
        "PassTraffic|1446": {
            $sum: "$1446.PassTraffic"
        },
        "PassTraffic|1447": {
            $sum: "$1447.PassTraffic"
        },
        "PassTraffic|1448": {
            $sum: "$1448.PassTraffic"
        },
        "PassTraffic|1449": {
            $sum: "$1449.PassTraffic"
        },
        "PassTraffic|1450": {
            $sum: "$1450.PassTraffic"
        },
        "PassTraffic|1451": {
            $sum: "$1451.PassTraffic"
        },
        "PassTraffic|1452": {
            $sum: "$1452.PassTraffic"
        },
        "PassTraffic|1453": {
            $sum: "$1453.PassTraffic"
        },
        "PassTraffic|1454": {
            $sum: "$1454.PassTraffic"
        },
        "PassTraffic|1455": {
            $sum: "$1455.PassTraffic"
        },
        "PassTraffic|1456": {
            $sum: "$1456.PassTraffic"
        },
        "PassTraffic|1457": {
            $sum: "$1457.PassTraffic"
        },
        "PassTraffic|1458": {
            $sum: "$1458.PassTraffic"
        },
        "PassTraffic|1459": {
            $sum: "$1459.PassTraffic"
        },
        "PassTraffic|1500": {
            $sum: "$1500.PassTraffic"
        },
        "PassTraffic|1501": {
            $sum: "$1501.PassTraffic"
        },
        "PassTraffic|1502": {
            $sum: "$1502.PassTraffic"
        },
        "PassTraffic|1503": {
            $sum: "$1503.PassTraffic"
        },
        "PassTraffic|1504": {
            $sum: "$1504.PassTraffic"
        },
        "PassTraffic|1505": {
            $sum: "$1505.PassTraffic"
        },
        "PassTraffic|1506": {
            $sum: "$1506.PassTraffic"
        },
        "PassTraffic|1507": {
            $sum: "$1507.PassTraffic"
        },
        "PassTraffic|1508": {
            $sum: "$1508.PassTraffic"
        },
        "PassTraffic|1509": {
            $sum: "$1509.PassTraffic"
        },
        "PassTraffic|1510": {
            $sum: "$1510.PassTraffic"
        },
        "PassTraffic|1511": {
            $sum: "$1511.PassTraffic"
        },
        "PassTraffic|1512": {
            $sum: "$1512.PassTraffic"
        },
        "PassTraffic|1513": {
            $sum: "$1513.PassTraffic"
        },
        "PassTraffic|1514": {
            $sum: "$1514.PassTraffic"
        },
        "PassTraffic|1515": {
            $sum: "$1515.PassTraffic"
        },
        "PassTraffic|1516": {
            $sum: "$1516.PassTraffic"
        },
        "PassTraffic|1517": {
            $sum: "$1517.PassTraffic"
        },
        "PassTraffic|1518": {
            $sum: "$1518.PassTraffic"
        },
        "PassTraffic|1519": {
            $sum: "$1519.PassTraffic"
        },
        "PassTraffic|1520": {
            $sum: "$1520.PassTraffic"
        },
        "PassTraffic|1521": {
            $sum: "$1521.PassTraffic"
        },
        "PassTraffic|1522": {
            $sum: "$1522.PassTraffic"
        },
        "PassTraffic|1523": {
            $sum: "$1523.PassTraffic"
        },
        "PassTraffic|1524": {
            $sum: "$1524.PassTraffic"
        },
        "PassTraffic|1525": {
            $sum: "$1525.PassTraffic"
        },
        "PassTraffic|1526": {
            $sum: "$1526.PassTraffic"
        },
        "PassTraffic|1527": {
            $sum: "$1527.PassTraffic"
        },
        "PassTraffic|1528": {
            $sum: "$1528.PassTraffic"
        },
        "PassTraffic|1529": {
            $sum: "$1529.PassTraffic"
        },
        "PassTraffic|1530": {
            $sum: "$1530.PassTraffic"
        },
        "PassTraffic|1531": {
            $sum: "$1531.PassTraffic"
        },
        "PassTraffic|1532": {
            $sum: "$1532.PassTraffic"
        },
        "PassTraffic|1533": {
            $sum: "$1533.PassTraffic"
        },
        "PassTraffic|1534": {
            $sum: "$1534.PassTraffic"
        },
        "PassTraffic|1535": {
            $sum: "$1535.PassTraffic"
        },
        "PassTraffic|1536": {
            $sum: "$1536.PassTraffic"
        },
        "PassTraffic|1537": {
            $sum: "$1537.PassTraffic"
        },
        "PassTraffic|1538": {
            $sum: "$1538.PassTraffic"
        },
        "PassTraffic|1539": {
            $sum: "$1539.PassTraffic"
        },
        "PassTraffic|1540": {
            $sum: "$1540.PassTraffic"
        },
        "PassTraffic|1541": {
            $sum: "$1541.PassTraffic"
        },
        "PassTraffic|1542": {
            $sum: "$1542.PassTraffic"
        },
        "PassTraffic|1543": {
            $sum: "$1543.PassTraffic"
        },
        "PassTraffic|1544": {
            $sum: "$1544.PassTraffic"
        },
        "PassTraffic|1545": {
            $sum: "$1545.PassTraffic"
        },
        "PassTraffic|1546": {
            $sum: "$1546.PassTraffic"
        },
        "PassTraffic|1547": {
            $sum: "$1547.PassTraffic"
        },
        "PassTraffic|1548": {
            $sum: "$1548.PassTraffic"
        },
        "PassTraffic|1549": {
            $sum: "$1549.PassTraffic"
        },
        "PassTraffic|1550": {
            $sum: "$1550.PassTraffic"
        },
        "PassTraffic|1551": {
            $sum: "$1551.PassTraffic"
        },
        "PassTraffic|1552": {
            $sum: "$1552.PassTraffic"
        },
        "PassTraffic|1553": {
            $sum: "$1553.PassTraffic"
        },
        "PassTraffic|1554": {
            $sum: "$1554.PassTraffic"
        },
        "PassTraffic|1555": {
            $sum: "$1555.PassTraffic"
        },
        "PassTraffic|1556": {
            $sum: "$1556.PassTraffic"
        },
        "PassTraffic|1557": {
            $sum: "$1557.PassTraffic"
        },
        "PassTraffic|1558": {
            $sum: "$1558.PassTraffic"
        },
        "PassTraffic|1559": {
            $sum: "$1559.PassTraffic"
        },
        "PassTraffic|1600": {
            $sum: "$1600.PassTraffic"
        },
        "PassTraffic|1601": {
            $sum: "$1601.PassTraffic"
        },
        "PassTraffic|1602": {
            $sum: "$1602.PassTraffic"
        },
        "PassTraffic|1603": {
            $sum: "$1603.PassTraffic"
        },
        "PassTraffic|1604": {
            $sum: "$1604.PassTraffic"
        },
        "PassTraffic|1605": {
            $sum: "$1605.PassTraffic"
        },
        "PassTraffic|1606": {
            $sum: "$1606.PassTraffic"
        },
        "PassTraffic|1607": {
            $sum: "$1607.PassTraffic"
        },
        "PassTraffic|1608": {
            $sum: "$1608.PassTraffic"
        },
        "PassTraffic|1609": {
            $sum: "$1609.PassTraffic"
        },
        "PassTraffic|1610": {
            $sum: "$1610.PassTraffic"
        },
        "PassTraffic|1611": {
            $sum: "$1611.PassTraffic"
        },
        "PassTraffic|1612": {
            $sum: "$1612.PassTraffic"
        },
        "PassTraffic|1613": {
            $sum: "$1613.PassTraffic"
        },
        "PassTraffic|1614": {
            $sum: "$1614.PassTraffic"
        },
        "PassTraffic|1615": {
            $sum: "$1615.PassTraffic"
        },
        "PassTraffic|1616": {
            $sum: "$1616.PassTraffic"
        },
        "PassTraffic|1617": {
            $sum: "$1617.PassTraffic"
        },
        "PassTraffic|1618": {
            $sum: "$1618.PassTraffic"
        },
        "PassTraffic|1619": {
            $sum: "$1619.PassTraffic"
        },
        "PassTraffic|1620": {
            $sum: "$1620.PassTraffic"
        },
        "PassTraffic|1621": {
            $sum: "$1621.PassTraffic"
        },
        "PassTraffic|1622": {
            $sum: "$1622.PassTraffic"
        },
        "PassTraffic|1623": {
            $sum: "$1623.PassTraffic"
        },
        "PassTraffic|1624": {
            $sum: "$1624.PassTraffic"
        },
        "PassTraffic|1625": {
            $sum: "$1625.PassTraffic"
        },
        "PassTraffic|1626": {
            $sum: "$1626.PassTraffic"
        },
        "PassTraffic|1627": {
            $sum: "$1627.PassTraffic"
        },
        "PassTraffic|1628": {
            $sum: "$1628.PassTraffic"
        },
        "PassTraffic|1629": {
            $sum: "$1629.PassTraffic"
        },
        "PassTraffic|1630": {
            $sum: "$1630.PassTraffic"
        },
        "PassTraffic|1631": {
            $sum: "$1631.PassTraffic"
        },
        "PassTraffic|1632": {
            $sum: "$1632.PassTraffic"
        },
        "PassTraffic|1633": {
            $sum: "$1633.PassTraffic"
        },
        "PassTraffic|1634": {
            $sum: "$1634.PassTraffic"
        },
        "PassTraffic|1635": {
            $sum: "$1635.PassTraffic"
        },
        "PassTraffic|1636": {
            $sum: "$1636.PassTraffic"
        },
        "PassTraffic|1637": {
            $sum: "$1637.PassTraffic"
        },
        "PassTraffic|1638": {
            $sum: "$1638.PassTraffic"
        },
        "PassTraffic|1639": {
            $sum: "$1639.PassTraffic"
        },
        "PassTraffic|1640": {
            $sum: "$1640.PassTraffic"
        },
        "PassTraffic|1641": {
            $sum: "$1641.PassTraffic"
        },
        "PassTraffic|1642": {
            $sum: "$1642.PassTraffic"
        },
        "PassTraffic|1643": {
            $sum: "$1643.PassTraffic"
        },
        "PassTraffic|1644": {
            $sum: "$1644.PassTraffic"
        },
        "PassTraffic|1645": {
            $sum: "$1645.PassTraffic"
        },
        "PassTraffic|1646": {
            $sum: "$1646.PassTraffic"
        },
        "PassTraffic|1647": {
            $sum: "$1647.PassTraffic"
        },
        "PassTraffic|1648": {
            $sum: "$1648.PassTraffic"
        },
        "PassTraffic|1649": {
            $sum: "$1649.PassTraffic"
        },
        "PassTraffic|1650": {
            $sum: "$1650.PassTraffic"
        },
        "PassTraffic|1651": {
            $sum: "$1651.PassTraffic"
        },
        "PassTraffic|1652": {
            $sum: "$1652.PassTraffic"
        },
        "PassTraffic|1653": {
            $sum: "$1653.PassTraffic"
        },
        "PassTraffic|1654": {
            $sum: "$1654.PassTraffic"
        },
        "PassTraffic|1655": {
            $sum: "$1655.PassTraffic"
        },
        "PassTraffic|1656": {
            $sum: "$1656.PassTraffic"
        },
        "PassTraffic|1657": {
            $sum: "$1657.PassTraffic"
        },
        "PassTraffic|1658": {
            $sum: "$1658.PassTraffic"
        },
        "PassTraffic|1659": {
            $sum: "$1659.PassTraffic"
        },
        "PassTraffic|1700": {
            $sum: "$1700.PassTraffic"
        },
        "PassTraffic|1701": {
            $sum: "$1701.PassTraffic"
        },
        "PassTraffic|1702": {
            $sum: "$1702.PassTraffic"
        },
        "PassTraffic|1703": {
            $sum: "$1703.PassTraffic"
        },
        "PassTraffic|1704": {
            $sum: "$1704.PassTraffic"
        },
        "PassTraffic|1705": {
            $sum: "$1705.PassTraffic"
        },
        "PassTraffic|1706": {
            $sum: "$1706.PassTraffic"
        },
        "PassTraffic|1707": {
            $sum: "$1707.PassTraffic"
        },
        "PassTraffic|1708": {
            $sum: "$1708.PassTraffic"
        },
        "PassTraffic|1709": {
            $sum: "$1709.PassTraffic"
        },
        "PassTraffic|1710": {
            $sum: "$1710.PassTraffic"
        },
        "PassTraffic|1711": {
            $sum: "$1711.PassTraffic"
        },
        "PassTraffic|1712": {
            $sum: "$1712.PassTraffic"
        },
        "PassTraffic|1713": {
            $sum: "$1713.PassTraffic"
        },
        "PassTraffic|1714": {
            $sum: "$1714.PassTraffic"
        },
        "PassTraffic|1715": {
            $sum: "$1715.PassTraffic"
        },
        "PassTraffic|1716": {
            $sum: "$1716.PassTraffic"
        },
        "PassTraffic|1717": {
            $sum: "$1717.PassTraffic"
        },
        "PassTraffic|1718": {
            $sum: "$1718.PassTraffic"
        },
        "PassTraffic|1719": {
            $sum: "$1719.PassTraffic"
        },
        "PassTraffic|1720": {
            $sum: "$1720.PassTraffic"
        },
        "PassTraffic|1721": {
            $sum: "$1721.PassTraffic"
        },
        "PassTraffic|1722": {
            $sum: "$1722.PassTraffic"
        },
        "PassTraffic|1723": {
            $sum: "$1723.PassTraffic"
        },
        "PassTraffic|1724": {
            $sum: "$1724.PassTraffic"
        },
        "PassTraffic|1725": {
            $sum: "$1725.PassTraffic"
        },
        "PassTraffic|1726": {
            $sum: "$1726.PassTraffic"
        },
        "PassTraffic|1727": {
            $sum: "$1727.PassTraffic"
        },
        "PassTraffic|1728": {
            $sum: "$1728.PassTraffic"
        },
        "PassTraffic|1729": {
            $sum: "$1729.PassTraffic"
        },
        "PassTraffic|1730": {
            $sum: "$1730.PassTraffic"
        },
        "PassTraffic|1731": {
            $sum: "$1731.PassTraffic"
        },
        "PassTraffic|1732": {
            $sum: "$1732.PassTraffic"
        },
        "PassTraffic|1733": {
            $sum: "$1733.PassTraffic"
        },
        "PassTraffic|1734": {
            $sum: "$1734.PassTraffic"
        },
        "PassTraffic|1735": {
            $sum: "$1735.PassTraffic"
        },
        "PassTraffic|1736": {
            $sum: "$1736.PassTraffic"
        },
        "PassTraffic|1737": {
            $sum: "$1737.PassTraffic"
        },
        "PassTraffic|1738": {
            $sum: "$1738.PassTraffic"
        },
        "PassTraffic|1739": {
            $sum: "$1739.PassTraffic"
        },
        "PassTraffic|1740": {
            $sum: "$1740.PassTraffic"
        },
        "PassTraffic|1741": {
            $sum: "$1741.PassTraffic"
        },
        "PassTraffic|1742": {
            $sum: "$1742.PassTraffic"
        },
        "PassTraffic|1743": {
            $sum: "$1743.PassTraffic"
        },
        "PassTraffic|1744": {
            $sum: "$1744.PassTraffic"
        },
        "PassTraffic|1745": {
            $sum: "$1745.PassTraffic"
        },
        "PassTraffic|1746": {
            $sum: "$1746.PassTraffic"
        },
        "PassTraffic|1747": {
            $sum: "$1747.PassTraffic"
        },
        "PassTraffic|1748": {
            $sum: "$1748.PassTraffic"
        },
        "PassTraffic|1749": {
            $sum: "$1749.PassTraffic"
        },
        "PassTraffic|1750": {
            $sum: "$1750.PassTraffic"
        },
        "PassTraffic|1751": {
            $sum: "$1751.PassTraffic"
        },
        "PassTraffic|1752": {
            $sum: "$1752.PassTraffic"
        },
        "PassTraffic|1753": {
            $sum: "$1753.PassTraffic"
        },
        "PassTraffic|1754": {
            $sum: "$1754.PassTraffic"
        },
        "PassTraffic|1755": {
            $sum: "$1755.PassTraffic"
        },
        "PassTraffic|1756": {
            $sum: "$1756.PassTraffic"
        },
        "PassTraffic|1757": {
            $sum: "$1757.PassTraffic"
        },
        "PassTraffic|1758": {
            $sum: "$1758.PassTraffic"
        },
        "PassTraffic|1759": {
            $sum: "$1759.PassTraffic"
        },
        "PassTraffic|1800": {
            $sum: "$1800.PassTraffic"
        },
        "PassTraffic|1801": {
            $sum: "$1801.PassTraffic"
        },
        "PassTraffic|1802": {
            $sum: "$1802.PassTraffic"
        },
        "PassTraffic|1803": {
            $sum: "$1803.PassTraffic"
        },
        "PassTraffic|1804": {
            $sum: "$1804.PassTraffic"
        },
        "PassTraffic|1805": {
            $sum: "$1805.PassTraffic"
        },
        "PassTraffic|1806": {
            $sum: "$1806.PassTraffic"
        },
        "PassTraffic|1807": {
            $sum: "$1807.PassTraffic"
        },
        "PassTraffic|1808": {
            $sum: "$1808.PassTraffic"
        },
        "PassTraffic|1809": {
            $sum: "$1809.PassTraffic"
        },
        "PassTraffic|1810": {
            $sum: "$1810.PassTraffic"
        },
        "PassTraffic|1811": {
            $sum: "$1811.PassTraffic"
        },
        "PassTraffic|1812": {
            $sum: "$1812.PassTraffic"
        },
        "PassTraffic|1813": {
            $sum: "$1813.PassTraffic"
        },
        "PassTraffic|1814": {
            $sum: "$1814.PassTraffic"
        },
        "PassTraffic|1815": {
            $sum: "$1815.PassTraffic"
        },
        "PassTraffic|1816": {
            $sum: "$1816.PassTraffic"
        },
        "PassTraffic|1817": {
            $sum: "$1817.PassTraffic"
        },
        "PassTraffic|1818": {
            $sum: "$1818.PassTraffic"
        },
        "PassTraffic|1819": {
            $sum: "$1819.PassTraffic"
        },
        "PassTraffic|1820": {
            $sum: "$1820.PassTraffic"
        },
        "PassTraffic|1821": {
            $sum: "$1821.PassTraffic"
        },
        "PassTraffic|1822": {
            $sum: "$1822.PassTraffic"
        },
        "PassTraffic|1823": {
            $sum: "$1823.PassTraffic"
        },
        "PassTraffic|1824": {
            $sum: "$1824.PassTraffic"
        },
        "PassTraffic|1825": {
            $sum: "$1825.PassTraffic"
        },
        "PassTraffic|1826": {
            $sum: "$1826.PassTraffic"
        },
        "PassTraffic|1827": {
            $sum: "$1827.PassTraffic"
        },
        "PassTraffic|1828": {
            $sum: "$1828.PassTraffic"
        },
        "PassTraffic|1829": {
            $sum: "$1829.PassTraffic"
        },
        "PassTraffic|1830": {
            $sum: "$1830.PassTraffic"
        },
        "PassTraffic|1831": {
            $sum: "$1831.PassTraffic"
        },
        "PassTraffic|1832": {
            $sum: "$1832.PassTraffic"
        },
        "PassTraffic|1833": {
            $sum: "$1833.PassTraffic"
        },
        "PassTraffic|1834": {
            $sum: "$1834.PassTraffic"
        },
        "PassTraffic|1835": {
            $sum: "$1835.PassTraffic"
        },
        "PassTraffic|1836": {
            $sum: "$1836.PassTraffic"
        },
        "PassTraffic|1837": {
            $sum: "$1837.PassTraffic"
        },
        "PassTraffic|1838": {
            $sum: "$1838.PassTraffic"
        },
        "PassTraffic|1839": {
            $sum: "$1839.PassTraffic"
        },
        "PassTraffic|1840": {
            $sum: "$1840.PassTraffic"
        },
        "PassTraffic|1841": {
            $sum: "$1841.PassTraffic"
        },
        "PassTraffic|1842": {
            $sum: "$1842.PassTraffic"
        },
        "PassTraffic|1843": {
            $sum: "$1843.PassTraffic"
        },
        "PassTraffic|1844": {
            $sum: "$1844.PassTraffic"
        },
        "PassTraffic|1845": {
            $sum: "$1845.PassTraffic"
        },
        "PassTraffic|1846": {
            $sum: "$1846.PassTraffic"
        },
        "PassTraffic|1847": {
            $sum: "$1847.PassTraffic"
        },
        "PassTraffic|1848": {
            $sum: "$1848.PassTraffic"
        },
        "PassTraffic|1849": {
            $sum: "$1849.PassTraffic"
        },
        "PassTraffic|1850": {
            $sum: "$1850.PassTraffic"
        },
        "PassTraffic|1851": {
            $sum: "$1851.PassTraffic"
        },
        "PassTraffic|1852": {
            $sum: "$1852.PassTraffic"
        },
        "PassTraffic|1853": {
            $sum: "$1853.PassTraffic"
        },
        "PassTraffic|1854": {
            $sum: "$1854.PassTraffic"
        },
        "PassTraffic|1855": {
            $sum: "$1855.PassTraffic"
        },
        "PassTraffic|1856": {
            $sum: "$1856.PassTraffic"
        },
        "PassTraffic|1857": {
            $sum: "$1857.PassTraffic"
        },
        "PassTraffic|1858": {
            $sum: "$1858.PassTraffic"
        },
        "PassTraffic|1859": {
            $sum: "$1859.PassTraffic"
        },
        "PassTraffic|1900": {
            $sum: "$1900.PassTraffic"
        },
        "PassTraffic|1901": {
            $sum: "$1901.PassTraffic"
        },
        "PassTraffic|1902": {
            $sum: "$1902.PassTraffic"
        },
        "PassTraffic|1903": {
            $sum: "$1903.PassTraffic"
        },
        "PassTraffic|1904": {
            $sum: "$1904.PassTraffic"
        },
        "PassTraffic|1905": {
            $sum: "$1905.PassTraffic"
        },
        "PassTraffic|1906": {
            $sum: "$1906.PassTraffic"
        },
        "PassTraffic|1907": {
            $sum: "$1907.PassTraffic"
        },
        "PassTraffic|1908": {
            $sum: "$1908.PassTraffic"
        },
        "PassTraffic|1909": {
            $sum: "$1909.PassTraffic"
        },
        "PassTraffic|1910": {
            $sum: "$1910.PassTraffic"
        },
        "PassTraffic|1911": {
            $sum: "$1911.PassTraffic"
        },
        "PassTraffic|1912": {
            $sum: "$1912.PassTraffic"
        },
        "PassTraffic|1913": {
            $sum: "$1913.PassTraffic"
        },
        "PassTraffic|1914": {
            $sum: "$1914.PassTraffic"
        },
        "PassTraffic|1915": {
            $sum: "$1915.PassTraffic"
        },
        "PassTraffic|1916": {
            $sum: "$1916.PassTraffic"
        },
        "PassTraffic|1917": {
            $sum: "$1917.PassTraffic"
        },
        "PassTraffic|1918": {
            $sum: "$1918.PassTraffic"
        },
        "PassTraffic|1919": {
            $sum: "$1919.PassTraffic"
        },
        "PassTraffic|1920": {
            $sum: "$1920.PassTraffic"
        },
        "PassTraffic|1921": {
            $sum: "$1921.PassTraffic"
        },
        "PassTraffic|1922": {
            $sum: "$1922.PassTraffic"
        },
        "PassTraffic|1923": {
            $sum: "$1923.PassTraffic"
        },
        "PassTraffic|1924": {
            $sum: "$1924.PassTraffic"
        },
        "PassTraffic|1925": {
            $sum: "$1925.PassTraffic"
        },
        "PassTraffic|1926": {
            $sum: "$1926.PassTraffic"
        },
        "PassTraffic|1927": {
            $sum: "$1927.PassTraffic"
        },
        "PassTraffic|1928": {
            $sum: "$1928.PassTraffic"
        },
        "PassTraffic|1929": {
            $sum: "$1929.PassTraffic"
        },
        "PassTraffic|1930": {
            $sum: "$1930.PassTraffic"
        },
        "PassTraffic|1931": {
            $sum: "$1931.PassTraffic"
        },
        "PassTraffic|1932": {
            $sum: "$1932.PassTraffic"
        },
        "PassTraffic|1933": {
            $sum: "$1933.PassTraffic"
        },
        "PassTraffic|1934": {
            $sum: "$1934.PassTraffic"
        },
        "PassTraffic|1935": {
            $sum: "$1935.PassTraffic"
        },
        "PassTraffic|1936": {
            $sum: "$1936.PassTraffic"
        },
        "PassTraffic|1937": {
            $sum: "$1937.PassTraffic"
        },
        "PassTraffic|1938": {
            $sum: "$1938.PassTraffic"
        },
        "PassTraffic|1939": {
            $sum: "$1939.PassTraffic"
        },
        "PassTraffic|1940": {
            $sum: "$1940.PassTraffic"
        },
        "PassTraffic|1941": {
            $sum: "$1941.PassTraffic"
        },
        "PassTraffic|1942": {
            $sum: "$1942.PassTraffic"
        },
        "PassTraffic|1943": {
            $sum: "$1943.PassTraffic"
        },
        "PassTraffic|1944": {
            $sum: "$1944.PassTraffic"
        },
        "PassTraffic|1945": {
            $sum: "$1945.PassTraffic"
        },
        "PassTraffic|1946": {
            $sum: "$1946.PassTraffic"
        },
        "PassTraffic|1947": {
            $sum: "$1947.PassTraffic"
        },
        "PassTraffic|1948": {
            $sum: "$1948.PassTraffic"
        },
        "PassTraffic|1949": {
            $sum: "$1949.PassTraffic"
        },
        "PassTraffic|1950": {
            $sum: "$1950.PassTraffic"
        },
        "PassTraffic|1951": {
            $sum: "$1951.PassTraffic"
        },
        "PassTraffic|1952": {
            $sum: "$1952.PassTraffic"
        },
        "PassTraffic|1953": {
            $sum: "$1953.PassTraffic"
        },
        "PassTraffic|1954": {
            $sum: "$1954.PassTraffic"
        },
        "PassTraffic|1955": {
            $sum: "$1955.PassTraffic"
        },
        "PassTraffic|1956": {
            $sum: "$1956.PassTraffic"
        },
        "PassTraffic|1957": {
            $sum: "$1957.PassTraffic"
        },
        "PassTraffic|1958": {
            $sum: "$1958.PassTraffic"
        },
        "PassTraffic|1959": {
            $sum: "$1959.PassTraffic"
        },
        "PassTraffic|2000": {
            $sum: "$2000.PassTraffic"
        },
        "PassTraffic|2001": {
            $sum: "$2001.PassTraffic"
        },
        "PassTraffic|2002": {
            $sum: "$2002.PassTraffic"
        },
        "PassTraffic|2003": {
            $sum: "$2003.PassTraffic"
        },
        "PassTraffic|2004": {
            $sum: "$2004.PassTraffic"
        },
        "PassTraffic|2005": {
            $sum: "$2005.PassTraffic"
        },
        "PassTraffic|2006": {
            $sum: "$2006.PassTraffic"
        },
        "PassTraffic|2007": {
            $sum: "$2007.PassTraffic"
        },
        "PassTraffic|2008": {
            $sum: "$2008.PassTraffic"
        },
        "PassTraffic|2009": {
            $sum: "$2009.PassTraffic"
        },
        "PassTraffic|2010": {
            $sum: "$2010.PassTraffic"
        },
        "PassTraffic|2011": {
            $sum: "$2011.PassTraffic"
        },
        "PassTraffic|2012": {
            $sum: "$2012.PassTraffic"
        },
        "PassTraffic|2013": {
            $sum: "$2013.PassTraffic"
        },
        "PassTraffic|2014": {
            $sum: "$2014.PassTraffic"
        },
        "PassTraffic|2015": {
            $sum: "$2015.PassTraffic"
        },
        "PassTraffic|2016": {
            $sum: "$2016.PassTraffic"
        },
        "PassTraffic|2017": {
            $sum: "$2017.PassTraffic"
        },
        "PassTraffic|2018": {
            $sum: "$2018.PassTraffic"
        },
        "PassTraffic|2019": {
            $sum: "$2019.PassTraffic"
        },
        "PassTraffic|2020": {
            $sum: "$2020.PassTraffic"
        },
        "PassTraffic|2021": {
            $sum: "$2021.PassTraffic"
        },
        "PassTraffic|2022": {
            $sum: "$2022.PassTraffic"
        },
        "PassTraffic|2023": {
            $sum: "$2023.PassTraffic"
        },
        "PassTraffic|2024": {
            $sum: "$2024.PassTraffic"
        },
        "PassTraffic|2025": {
            $sum: "$2025.PassTraffic"
        },
        "PassTraffic|2026": {
            $sum: "$2026.PassTraffic"
        },
        "PassTraffic|2027": {
            $sum: "$2027.PassTraffic"
        },
        "PassTraffic|2028": {
            $sum: "$2028.PassTraffic"
        },
        "PassTraffic|2029": {
            $sum: "$2029.PassTraffic"
        },
        "PassTraffic|2030": {
            $sum: "$2030.PassTraffic"
        },
        "PassTraffic|2031": {
            $sum: "$2031.PassTraffic"
        },
        "PassTraffic|2032": {
            $sum: "$2032.PassTraffic"
        },
        "PassTraffic|2033": {
            $sum: "$2033.PassTraffic"
        },
        "PassTraffic|2034": {
            $sum: "$2034.PassTraffic"
        },
        "PassTraffic|2035": {
            $sum: "$2035.PassTraffic"
        },
        "PassTraffic|2036": {
            $sum: "$2036.PassTraffic"
        },
        "PassTraffic|2037": {
            $sum: "$2037.PassTraffic"
        },
        "PassTraffic|2038": {
            $sum: "$2038.PassTraffic"
        },
        "PassTraffic|2039": {
            $sum: "$2039.PassTraffic"
        },
        "PassTraffic|2040": {
            $sum: "$2040.PassTraffic"
        },
        "PassTraffic|2041": {
            $sum: "$2041.PassTraffic"
        },
        "PassTraffic|2042": {
            $sum: "$2042.PassTraffic"
        },
        "PassTraffic|2043": {
            $sum: "$2043.PassTraffic"
        },
        "PassTraffic|2044": {
            $sum: "$2044.PassTraffic"
        },
        "PassTraffic|2045": {
            $sum: "$2045.PassTraffic"
        },
        "PassTraffic|2046": {
            $sum: "$2046.PassTraffic"
        },
        "PassTraffic|2047": {
            $sum: "$2047.PassTraffic"
        },
        "PassTraffic|2048": {
            $sum: "$2048.PassTraffic"
        },
        "PassTraffic|2049": {
            $sum: "$2049.PassTraffic"
        },
        "PassTraffic|2050": {
            $sum: "$2050.PassTraffic"
        },
        "PassTraffic|2051": {
            $sum: "$2051.PassTraffic"
        },
        "PassTraffic|2052": {
            $sum: "$2052.PassTraffic"
        },
        "PassTraffic|2053": {
            $sum: "$2053.PassTraffic"
        },
        "PassTraffic|2054": {
            $sum: "$2054.PassTraffic"
        },
        "PassTraffic|2055": {
            $sum: "$2055.PassTraffic"
        },
        "PassTraffic|2056": {
            $sum: "$2056.PassTraffic"
        },
        "PassTraffic|2057": {
            $sum: "$2057.PassTraffic"
        },
        "PassTraffic|2058": {
            $sum: "$2058.PassTraffic"
        },
        "PassTraffic|2059": {
            $sum: "$2059.PassTraffic"
        },
        "PassTraffic|2100": {
            $sum: "$2100.PassTraffic"
        },
        "PassTraffic|2101": {
            $sum: "$2101.PassTraffic"
        },
        "PassTraffic|2102": {
            $sum: "$2102.PassTraffic"
        },
        "PassTraffic|2103": {
            $sum: "$2103.PassTraffic"
        },
        "PassTraffic|2104": {
            $sum: "$2104.PassTraffic"
        },
        "PassTraffic|2105": {
            $sum: "$2105.PassTraffic"
        },
        "PassTraffic|2106": {
            $sum: "$2106.PassTraffic"
        },
        "PassTraffic|2107": {
            $sum: "$2107.PassTraffic"
        },
        "PassTraffic|2108": {
            $sum: "$2108.PassTraffic"
        },
        "PassTraffic|2109": {
            $sum: "$2109.PassTraffic"
        },
        "PassTraffic|2110": {
            $sum: "$2110.PassTraffic"
        },
        "PassTraffic|2111": {
            $sum: "$2111.PassTraffic"
        },
        "PassTraffic|2112": {
            $sum: "$2112.PassTraffic"
        },
        "PassTraffic|2113": {
            $sum: "$2113.PassTraffic"
        },
        "PassTraffic|2114": {
            $sum: "$2114.PassTraffic"
        },
        "PassTraffic|2115": {
            $sum: "$2115.PassTraffic"
        },
        "PassTraffic|2116": {
            $sum: "$2116.PassTraffic"
        },
        "PassTraffic|2117": {
            $sum: "$2117.PassTraffic"
        },
        "PassTraffic|2118": {
            $sum: "$2118.PassTraffic"
        },
        "PassTraffic|2119": {
            $sum: "$2119.PassTraffic"
        },
        "PassTraffic|2120": {
            $sum: "$2120.PassTraffic"
        },
        "PassTraffic|2121": {
            $sum: "$2121.PassTraffic"
        },
        "PassTraffic|2122": {
            $sum: "$2122.PassTraffic"
        },
        "PassTraffic|2123": {
            $sum: "$2123.PassTraffic"
        },
        "PassTraffic|2124": {
            $sum: "$2124.PassTraffic"
        },
        "PassTraffic|2125": {
            $sum: "$2125.PassTraffic"
        },
        "PassTraffic|2126": {
            $sum: "$2126.PassTraffic"
        },
        "PassTraffic|2127": {
            $sum: "$2127.PassTraffic"
        },
        "PassTraffic|2128": {
            $sum: "$2128.PassTraffic"
        },
        "PassTraffic|2129": {
            $sum: "$2129.PassTraffic"
        },
        "PassTraffic|2130": {
            $sum: "$2130.PassTraffic"
        },
        "PassTraffic|2131": {
            $sum: "$2131.PassTraffic"
        },
        "PassTraffic|2132": {
            $sum: "$2132.PassTraffic"
        },
        "PassTraffic|2133": {
            $sum: "$2133.PassTraffic"
        },
        "PassTraffic|2134": {
            $sum: "$2134.PassTraffic"
        },
        "PassTraffic|2135": {
            $sum: "$2135.PassTraffic"
        },
        "PassTraffic|2136": {
            $sum: "$2136.PassTraffic"
        },
        "PassTraffic|2137": {
            $sum: "$2137.PassTraffic"
        },
        "PassTraffic|2138": {
            $sum: "$2138.PassTraffic"
        },
        "PassTraffic|2139": {
            $sum: "$2139.PassTraffic"
        },
        "PassTraffic|2140": {
            $sum: "$2140.PassTraffic"
        },
        "PassTraffic|2141": {
            $sum: "$2141.PassTraffic"
        },
        "PassTraffic|2142": {
            $sum: "$2142.PassTraffic"
        },
        "PassTraffic|2143": {
            $sum: "$2143.PassTraffic"
        },
        "PassTraffic|2144": {
            $sum: "$2144.PassTraffic"
        },
        "PassTraffic|2145": {
            $sum: "$2145.PassTraffic"
        },
        "PassTraffic|2146": {
            $sum: "$2146.PassTraffic"
        },
        "PassTraffic|2147": {
            $sum: "$2147.PassTraffic"
        },
        "PassTraffic|2148": {
            $sum: "$2148.PassTraffic"
        },
        "PassTraffic|2149": {
            $sum: "$2149.PassTraffic"
        },
        "PassTraffic|2150": {
            $sum: "$2150.PassTraffic"
        },
        "PassTraffic|2151": {
            $sum: "$2151.PassTraffic"
        },
        "PassTraffic|2152": {
            $sum: "$2152.PassTraffic"
        },
        "PassTraffic|2153": {
            $sum: "$2153.PassTraffic"
        },
        "PassTraffic|2154": {
            $sum: "$2154.PassTraffic"
        },
        "PassTraffic|2155": {
            $sum: "$2155.PassTraffic"
        },
        "PassTraffic|2156": {
            $sum: "$2156.PassTraffic"
        },
        "PassTraffic|2157": {
            $sum: "$2157.PassTraffic"
        },
        "PassTraffic|2158": {
            $sum: "$2158.PassTraffic"
        },
        "PassTraffic|2159": {
            $sum: "$2159.PassTraffic"
        },
        "PassTraffic|2200": {
            $sum: "$2200.PassTraffic"
        },
        "PassTraffic|2201": {
            $sum: "$2201.PassTraffic"
        },
        "PassTraffic|2202": {
            $sum: "$2202.PassTraffic"
        },
        "PassTraffic|2203": {
            $sum: "$2203.PassTraffic"
        },
        "PassTraffic|2204": {
            $sum: "$2204.PassTraffic"
        },
        "PassTraffic|2205": {
            $sum: "$2205.PassTraffic"
        },
        "PassTraffic|2206": {
            $sum: "$2206.PassTraffic"
        },
        "PassTraffic|2207": {
            $sum: "$2207.PassTraffic"
        },
        "PassTraffic|2208": {
            $sum: "$2208.PassTraffic"
        },
        "PassTraffic|2209": {
            $sum: "$2209.PassTraffic"
        },
        "PassTraffic|2210": {
            $sum: "$2210.PassTraffic"
        },
        "PassTraffic|2211": {
            $sum: "$2211.PassTraffic"
        },
        "PassTraffic|2212": {
            $sum: "$2212.PassTraffic"
        },
        "PassTraffic|2213": {
            $sum: "$2213.PassTraffic"
        },
        "PassTraffic|2214": {
            $sum: "$2214.PassTraffic"
        },
        "PassTraffic|2215": {
            $sum: "$2215.PassTraffic"
        },
        "PassTraffic|2216": {
            $sum: "$2216.PassTraffic"
        },
        "PassTraffic|2217": {
            $sum: "$2217.PassTraffic"
        },
        "PassTraffic|2218": {
            $sum: "$2218.PassTraffic"
        },
        "PassTraffic|2219": {
            $sum: "$2219.PassTraffic"
        },
        "PassTraffic|2220": {
            $sum: "$2220.PassTraffic"
        },
        "PassTraffic|2221": {
            $sum: "$2221.PassTraffic"
        },
        "PassTraffic|2222": {
            $sum: "$2222.PassTraffic"
        },
        "PassTraffic|2223": {
            $sum: "$2223.PassTraffic"
        },
        "PassTraffic|2224": {
            $sum: "$2224.PassTraffic"
        },
        "PassTraffic|2225": {
            $sum: "$2225.PassTraffic"
        },
        "PassTraffic|2226": {
            $sum: "$2226.PassTraffic"
        },
        "PassTraffic|2227": {
            $sum: "$2227.PassTraffic"
        },
        "PassTraffic|2228": {
            $sum: "$2228.PassTraffic"
        },
        "PassTraffic|2229": {
            $sum: "$2229.PassTraffic"
        },
        "PassTraffic|2230": {
            $sum: "$2230.PassTraffic"
        },
        "PassTraffic|2231": {
            $sum: "$2231.PassTraffic"
        },
        "PassTraffic|2232": {
            $sum: "$2232.PassTraffic"
        },
        "PassTraffic|2233": {
            $sum: "$2233.PassTraffic"
        },
        "PassTraffic|2234": {
            $sum: "$2234.PassTraffic"
        },
        "PassTraffic|2235": {
            $sum: "$2235.PassTraffic"
        },
        "PassTraffic|2236": {
            $sum: "$2236.PassTraffic"
        },
        "PassTraffic|2237": {
            $sum: "$2237.PassTraffic"
        },
        "PassTraffic|2238": {
            $sum: "$2238.PassTraffic"
        },
        "PassTraffic|2239": {
            $sum: "$2239.PassTraffic"
        },
        "PassTraffic|2240": {
            $sum: "$2240.PassTraffic"
        },
        "PassTraffic|2241": {
            $sum: "$2241.PassTraffic"
        },
        "PassTraffic|2242": {
            $sum: "$2242.PassTraffic"
        },
        "PassTraffic|2243": {
            $sum: "$2243.PassTraffic"
        },
        "PassTraffic|2244": {
            $sum: "$2244.PassTraffic"
        },
        "PassTraffic|2245": {
            $sum: "$2245.PassTraffic"
        },
        "PassTraffic|2246": {
            $sum: "$2246.PassTraffic"
        },
        "PassTraffic|2247": {
            $sum: "$2247.PassTraffic"
        },
        "PassTraffic|2248": {
            $sum: "$2248.PassTraffic"
        },
        "PassTraffic|2249": {
            $sum: "$2249.PassTraffic"
        },
        "PassTraffic|2250": {
            $sum: "$2250.PassTraffic"
        },
        "PassTraffic|2251": {
            $sum: "$2251.PassTraffic"
        },
        "PassTraffic|2252": {
            $sum: "$2252.PassTraffic"
        },
        "PassTraffic|2253": {
            $sum: "$2253.PassTraffic"
        },
        "PassTraffic|2254": {
            $sum: "$2254.PassTraffic"
        },
        "PassTraffic|2255": {
            $sum: "$2255.PassTraffic"
        },
        "PassTraffic|2256": {
            $sum: "$2256.PassTraffic"
        },
        "PassTraffic|2257": {
            $sum: "$2257.PassTraffic"
        },
        "PassTraffic|2258": {
            $sum: "$2258.PassTraffic"
        },
        "PassTraffic|2259": {
            $sum: "$2259.PassTraffic"
        },
        "PassTraffic|2300": {
            $sum: "$2300.PassTraffic"
        },
        "PassTraffic|2301": {
            $sum: "$2301.PassTraffic"
        },
        "PassTraffic|2302": {
            $sum: "$2302.PassTraffic"
        },
        "PassTraffic|2303": {
            $sum: "$2303.PassTraffic"
        },
        "PassTraffic|2304": {
            $sum: "$2304.PassTraffic"
        },
        "PassTraffic|2305": {
            $sum: "$2305.PassTraffic"
        },
        "PassTraffic|2306": {
            $sum: "$2306.PassTraffic"
        },
        "PassTraffic|2307": {
            $sum: "$2307.PassTraffic"
        },
        "PassTraffic|2308": {
            $sum: "$2308.PassTraffic"
        },
        "PassTraffic|2309": {
            $sum: "$2309.PassTraffic"
        },
        "PassTraffic|2310": {
            $sum: "$2310.PassTraffic"
        },
        "PassTraffic|2311": {
            $sum: "$2311.PassTraffic"
        },
        "PassTraffic|2312": {
            $sum: "$2312.PassTraffic"
        },
        "PassTraffic|2313": {
            $sum: "$2313.PassTraffic"
        },
        "PassTraffic|2314": {
            $sum: "$2314.PassTraffic"
        },
        "PassTraffic|2315": {
            $sum: "$2315.PassTraffic"
        },
        "PassTraffic|2316": {
            $sum: "$2316.PassTraffic"
        },
        "PassTraffic|2317": {
            $sum: "$2317.PassTraffic"
        },
        "PassTraffic|2318": {
            $sum: "$2318.PassTraffic"
        },
        "PassTraffic|2319": {
            $sum: "$2319.PassTraffic"
        },
        "PassTraffic|2320": {
            $sum: "$2320.PassTraffic"
        },
        "PassTraffic|2321": {
            $sum: "$2321.PassTraffic"
        },
        "PassTraffic|2322": {
            $sum: "$2322.PassTraffic"
        },
        "PassTraffic|2323": {
            $sum: "$2323.PassTraffic"
        },
        "PassTraffic|2324": {
            $sum: "$2324.PassTraffic"
        },
        "PassTraffic|2325": {
            $sum: "$2325.PassTraffic"
        },
        "PassTraffic|2326": {
            $sum: "$2326.PassTraffic"
        },
        "PassTraffic|2327": {
            $sum: "$2327.PassTraffic"
        },
        "PassTraffic|2328": {
            $sum: "$2328.PassTraffic"
        },
        "PassTraffic|2329": {
            $sum: "$2329.PassTraffic"
        },
        "PassTraffic|2330": {
            $sum: "$2330.PassTraffic"
        },
        "PassTraffic|2331": {
            $sum: "$2331.PassTraffic"
        },
        "PassTraffic|2332": {
            $sum: "$2332.PassTraffic"
        },
        "PassTraffic|2333": {
            $sum: "$2333.PassTraffic"
        },
        "PassTraffic|2334": {
            $sum: "$2334.PassTraffic"
        },
        "PassTraffic|2335": {
            $sum: "$2335.PassTraffic"
        },
        "PassTraffic|2336": {
            $sum: "$2336.PassTraffic"
        },
        "PassTraffic|2337": {
            $sum: "$2337.PassTraffic"
        },
        "PassTraffic|2338": {
            $sum: "$2338.PassTraffic"
        },
        "PassTraffic|2339": {
            $sum: "$2339.PassTraffic"
        },
        "PassTraffic|2340": {
            $sum: "$2340.PassTraffic"
        },
        "PassTraffic|2341": {
            $sum: "$2341.PassTraffic"
        },
        "PassTraffic|2342": {
            $sum: "$2342.PassTraffic"
        },
        "PassTraffic|2343": {
            $sum: "$2343.PassTraffic"
        },
        "PassTraffic|2344": {
            $sum: "$2344.PassTraffic"
        },
        "PassTraffic|2345": {
            $sum: "$2345.PassTraffic"
        },
        "PassTraffic|2346": {
            $sum: "$2346.PassTraffic"
        },
        "PassTraffic|2347": {
            $sum: "$2347.PassTraffic"
        },
        "PassTraffic|2348": {
            $sum: "$2348.PassTraffic"
        },
        "PassTraffic|2349": {
            $sum: "$2349.PassTraffic"
        },
        "PassTraffic|2350": {
            $sum: "$2350.PassTraffic"
        },
        "PassTraffic|2351": {
            $sum: "$2351.PassTraffic"
        },
        "PassTraffic|2352": {
            $sum: "$2352.PassTraffic"
        },
        "PassTraffic|2353": {
            $sum: "$2353.PassTraffic"
        },
        "PassTraffic|2354": {
            $sum: "$2354.PassTraffic"
        },
        "PassTraffic|2355": {
            $sum: "$2355.PassTraffic"
        },
        "PassTraffic|2356": {
            $sum: "$2356.PassTraffic"
        },
        "PassTraffic|2357": {
            $sum: "$2357.PassTraffic"
        },
        "PassTraffic|2358": {
            $sum: "$2358.PassTraffic"
        },
        "PassTraffic|2359": {
            $sum: "$2359.PassTraffic"
        }
    }
}, {
    $project: {
        "data": {
            $objectToArray: "$$ROOT"
        }
    }
}, {
    $project: {
        "data": {
            $filter: {
                input: "$data",
                as: "item",
                cond: {
                    $ne: ["$$item.k", "_id"]
                }
            }
        }
    }
}, {
    $unwind: "$data"
}, {
    $group: {
        "_id": {
            "key": "$_id",
            "field": {
                $arrayElemAt: [{
                    $split: ["$data.k", "|"]
                }, 0]
            },
            "time": {
                $arrayElemAt: [{
                    $split: ["$data.k", "|"]
                }, 1]
            }
        },
        "data": {
            $sum: "$data.v"
        }
    }
}, {
    $group: {
        "_id": {
            "key": "$_id.key",
            "time": "$_id.time"
        },
        "data": {
            $push: {
                k: "$_id.field",
                v: "$data"
            }
        }
    }
}, {
    $project: {
        "data": 1,
        "_id": {
            $toInt: {
                $add: [
                    "$_id.key",
                    {
                        $multiply: [
                            {
                                $floor: {
                                    $divide: [{
                                        $toInt: "$_id.time"
                                    }, 100]
                                }
                            },
                            3600
                        ]
                    },
                    {
                        $multiply: [
                            {
                                $mod: [{
                                    $toInt: "$_id.time"
                                }, 100]
                            },
                            60
                        ]
                    }
                ]
            }
        },
        
    }
}, {
    $replaceRoot: {
        newRoot: {
            $mergeObjects: [
                "$$ROOT",
                {
                    $arrayToObject: "$data"
                }
            ]
        }
    }
}, {
    $project: {
        "_id": 0,
        "timestamp": "$_id",
        "Traffic": "$Traffic",
        "IPV6Traffic": "$IPV6Traffic",
        "PassTraffic": "$PassTraffic",
        "HttpsTraffic": "$HttpsTraffic"
    }
}, {
    $sort: {
        "timestamp": 1
    }
}])
```
