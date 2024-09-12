
https://x.com/uCx4CoB9zdsu6H7

#!/bin/bash

while true; do

    response=$(curl -s https://mempool.fractalbitcoin.io/api/v1/fees/mempool-blocks)
    
    fastestFee=$(echo $response | jq '.[0].feeRange | .[-3]') 
    
    fastestFee=$(echo $response | jq '.[0].feeRange | .[-4]')
    
    echo $fastestFee

if awk "BEGIN {exit !($fastestFee < 2000)}"
# You can change the value of 2000

then

 command="yarn cli mint -i 45ee725c2c5993b3e4d308842d87e973bf1951f5f7a804b21e4dd964ecd12d6b_0 5 --fee-rate $fastestFee" 

 $command 

else

 echo "gasfee > 2000 . waiting for next check!"
 
 fi

    if [ $? -ne 0 ]; then
        echo "Command error, exit and run"
        exit 1
    fi

    sleep 120
    # If you are worried about merges caused by too many submissions of the same block, you can adjust the interval appropriately.
done
