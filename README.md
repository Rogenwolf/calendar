# calendar
printCal()
{
          year=$1
          month=$2
          allDay=0
          i=1990
          array=(0 31 0 31 30 31 30 31 31 30 31 30 31)
          while [ $i -lt $year ]
          do
                    if [[ `expr $i % 4` == 0 && `expr $i % 100` != 0 ]] || [ `expr $i % 400` == 0 ]
                    then
                              let allDay=allDay+366
                    else
                              let allDay=allDay+365
                    fi
                    let i++
          done

          if [[ `expr $year % 4` == 0 && `expr $year % 100` != 0 ]] || [ `expr $year % 400` == 0 ]
          then
                    array[2]=29
          else
                    array[2]=28
          fi
          i=1
          while [ $i -lt $month ]
          do
                    let allDay=allDay+array[i]
                    let i++
          done
          let allDay=allDay+1
          let week=allDay%7
          printf "Sun\tMon\tTue\tWed\tThr\tFir\tSat\t\n"
          blank=1
          column=0
          while [ $blank -le $week ]
          do
                    printf "\t"
                              let blank++
                              let column++
          done
          i=1
          while [ $i -le ${array[$month]} ]
          do
                    printf "$i\t"
                    let i++
                    let column++
                    if [ `expr $column % 7` == 0 ]
                    then
                              printf "\n"
                    fi
          done
          if [ `expr $column % 7` != 0 ]
          then     
                    printf "\n"
          fi

}

if [ $# -eq 0 ]
then
     year=`date +%Y`
     month=`date +%m`
elif [ $# -eq 1 ]
then
     echo "program not finished"
elif [ $# -eq 2 ]
then
     year=$1
     month=$2
else
     echo "too many arguments"
fi
printCal $year $month
