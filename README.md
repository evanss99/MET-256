# MET-256
program TemperatureConversion
  implicit none
  
  character(50) :: file_name
  integer :: i, num_values
  real :: celsius, kelvin
  character(len=100) :: line
  integer, parameter :: num_values_max = 100
  real, dimension(num_values_max) :: temperature_celsius, temperature_kelvin
  
  ! Open the file
  file_name = "Air-Temperature.csv"
  open(unit=10, file=file_name, status='old', action='read')
  
  ! Read temperature values from the file
  num_values = 0
  do
    read(10, '(A)', iostat=i) line
    if (i < 0) exit
    num_values = num_values + 1
    read(line, *) temperature_celsius(num_values)
  end do
  
  ! Convert Celsius to Kelvin
  do i = 1, num_values
    celsius = temperature_celsius(i)
    kelvin = celsius + 273.15
    temperature_kelvin(i) = kelvin
  end do
  
  ! Print the converted temperature values
  do i = 1, num_values
    write(*, *) "Temperature in Celsius:", temperature_celsius(i)
    write(*, *) "Temperature in Kelvin:", temperature_kelvin(i)
  end do
  
  ! Close the file
  close(10)
  
end program TemperatureConversion
