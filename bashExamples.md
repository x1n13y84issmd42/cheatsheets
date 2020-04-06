### Print $PATH as array
`readarray -d ":" -t ARR <<< $PATH && for p in ${ARR[@]}; do echo $p; done`