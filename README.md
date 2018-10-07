# RentWheels
RentWheels – A car rental system 

The system, RentWheels, rents a car to a user for certain duration.
A user is a person who can rent a car from one of the many available locations. Details of the user, like First name, last name, phone number, email, user type (admin or customer), password is recorded in the system. Additionally, every user must have an account, which will maintain details license number and if the user is in the system or deleted.


A user can rent a car of a certain type from a location. A car can be of many types (hatchback, sedan or SUV). It also has a unique car number, a manufacturer, color, year of make, and an availability flag which denotes if the car is available for booking.
Each car type has seating capacity (size : hatchback sedan or SUV). Each size has a different rate price. Many cars are available in one location. The company allows users to pick up cars from different locations. A car has certain details which are recorded in the system, such as brand, model, the price associated with each car. 

Each location has a unique location zip, name and address.
A user can book a car from any of the many locations, and has to return the car to the same location.
A user can book a particular car for a specific duration. The system records the date when the car is booked, along with the pickup and return date of the car. Each booking has a status (booked, confirmed, paid, and cancelled). 
For a particular booking, a user can make a payment using his/her card. The details of that is recorded in the system.








Database Structure

![ERDiagram](ImageCaptures/ERDiagram.PNG?raw=true "ER Diagram")
      


The database ,’digiashi_CarRental’ uses the following tables. 
cr_car
cr_user
cr_locations
cr_color
cr_car_location
cr_mfg
cr_payment
cr_size
cr_user
cr_booking

Mapping

![Mapping](ImageCaptures/Mapping.PNG?raw=true "Mapping")





Relational Schema

SQL Statements
-- phpMyAdmin SQL Dump
-- version 4.6.4
-- https://www.phpmyadmin.net/
--
-- Host: localhost
-- Database: `digiashi_CarRental`
--
-- --------------------------------------------------------
--
-- Table structure for table `cr_booking`
--

CREATE TABLE `cr_booking` (
  `booking_id` int(11) NOT NULL,
  `booking_pickup_location` varchar(11) NOT NULL,
  `booking_date` datetime NOT NULL,
  `booking_from_date` datetime NOT NULL,
  `booking_to_date` datetime NOT NULL,
  `car_no` varchar(11) NOT NULL,
  `user_id` int(11) NOT NULL,
  `booking_status` text NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `cr_booking`
--

INSERT INTO `cr_booking` (`booking_id`, `booking_pickup_location`, `booking_date`, `booking_from_date`, `booking_to_date`, `car_no`, `user_id`, `booking_status`) VALUES
(1, 'Dallas', '2016-12-05 08:10:18', '2016-12-06 00:00:00', '2016-12-08 23:59:59', 'CA 13 DEF', 7, 'Successful'),
(2, 'Irving', '2016-12-05 08:25:49', '2016-12-07 00:00:00', '2016-12-14 23:59:59', 'TX 15 RTY', 2, 'Successful'),
(3, 'Irving', '2016-12-05 08:28:49', '0000-00-00 00:00:00', '0000-00-00 00:00:00', 'TX 10 TR4', 2, 'Inprogress'),
(4, 'Austin', '2016-12-05 09:13:52', '2016-12-06 00:00:00', '2016-12-08 23:59:59', 'Ap 10 AN 96', 8, 'Successful');

-- --------------------------------------------------------

--
-- Table structure for table `cr_car`
--

CREATE TABLE `cr_car` (
  `car_no` varchar(255) NOT NULL,
  `mfg_id` int(255) NOT NULL,
  `color_id` int(100) NOT NULL,
  `year` int(4) NOT NULL,
  `car_availableFl` varchar(1) NOT NULL DEFAULT 'Y'
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `cr_car`
--

INSERT INTO `cr_car` (`car_no`, `mfg_id`, `color_id`, `year`, `car_availableFl`) VALUES
('Ap 10 AN 9608', 1, 1, 2011, 'N'),
('CA 10 AP 6789', 1, 1, 2016, 'Y'),
('CA 13 DEF', 3, 2, 2015, 'Y'),
('DA 12 ABC', 2, 1, 2013, 'Y'),
('FL 88 DNO', 2, 3, 2016, 'Y'),
('TX 02 THG', 2, 2, 2013, 'N'),
 ('TX 567 ED', 6, 2, 2015, 'Y'),
('TX 678 GH', 5, 4, 2012, 'N'),
('ww 12ww1234', 18, 1, 2016, 'Y'),
('XYZ123123', 2, 1, 2016, 'Y');

-- --------------------------------------------------------

--
-- Table structure for table `cr_car_location`
--

CREATE TABLE `cr_car_location` (
  `location_zip` int(10) NOT NULL,
  `car_no` varchar(255) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `cr_car_location`
--

INSERT INTO `cr_car_location` (`location_zip`, `car_no`) VALUES
(75248, 'Ap 10 AN 9608'),
(75248, 'CA 10 AP 6789'),
(75248, 'CA 13 DEF'),
 (77032, 'ww 12ww1234'),
(75248, 'XYZ123123');

-- --------------------------------------------------------

--
-- Table structure for table `cr_color`
--

CREATE TABLE `cr_color` (
  `color_id` int(255) NOT NULL,
  `color_name` text NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `cr_color`
--

INSERT INTO `cr_color` (`color_id`, `color_name`) VALUES
(1, 'Red'),
(2, 'Blue'),
(3, 'Black'),
(4, 'White');

-- --------------------------------------------------------

--
-- Table structure for table `cr_locations`
--

CREATE TABLE `cr_locations` (
  `location_zip` int(10) NOT NULL,
  `location_city` text NOT NULL,
  `location_address` longtext NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `cr_locations`
--

INSERT INTO `cr_locations` (`location_zip`, `location_city`, `location_address`) VALUES
(75038, 'Irving', ' 4002 N Belt Line Rd, Irving, TX 75038'),
(75248, 'Austin', 'Austin, TX 78712'),
(75251, 'McCallum', 'McCallum Blvd'),
(75252, 'Dallas', '800 W Campbell Rd, Richardson, TX 75080'),
(77032, 'Houston', '2800 N Terminal Rd, Houston, TX 77032');

-- --------------------------------------------------------

--
-- Table structure for table `cr_mfg`
--

CREATE TABLE `cr_mfg` (
  `mfg_id` int(255) NOT NULL,
  `mfg_brand` text NOT NULL,
  `mfg_model` varchar(255) NOT NULL,
  `mfg_rate` int(255) NOT NULL,
  `size_id` int(255) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `cr_mfg`
--

INSERT INTO `cr_mfg` (`mfg_id`, `mfg_brand`, `mfg_model`, `mfg_rate`, `size_id`) VALUES
(1, 'Toyota', 'Corolla', 15, 2),
(2, 'Toyota', 'Camry', 16, 2),
(3, 'Ford', 'Focus', 8, 1),
(4, 'Honda', 'Fit', 8, 1),
(5, 'BMW', 'X6', 15, 2)
-- --------------------------------------------------------
--
-- Table structure for table `cr_payment`
--

CREATE TABLE `cr_payment` (
  `payment_id` int(200) NOT NULL,
  `booking_id` int(200) NOT NULL,
  `payment_start_time` datetime NOT NULL,
  `payment_end_time` datetime NOT NULL,
  `price` double NOT NULL,
  `payment_status` text NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `cr_payment`
--

INSERT INTO `cr_payment` (`payment_id`, `booking_id`, `payment_start_time`, `payment_end_time`, `price`, `payment_status`) VALUES
(16, 1, '2016-12-05 08:11:03', '2016-12-05 08:11:03', 16, 'Successful'),
(17, 2, '2016-12-05 08:30:27', '2016-12-05 08:30:27', 0, 'Successful'),
(18, 4, '2016-12-05 09:14:55', '2016-12-05 09:14:55', 30, 'Successful');

-- --------------------------------------------------------

--
-- Table structure for table `cr_size`
--

CREATE TABLE `cr_size` (
  `size_id` int(255) NOT NULL,
  `size_detail` varchar(255) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `cr_size`
--

INSERT INTO `cr_size` (`size_id`, `size_detail`) VALUES
(1, 'Hatchback'),
(2, 'Sedan'),
(3, 'SUV');

-- --------------------------------------------------------

--
-- Table structure for table `cr_user`
--

CREATE TABLE `cr_user` (
  `user_id` int(11) NOT NULL,
  `user_firstname` varchar(25) NOT NULL,
  `user_lastname` varchar(25) NOT NULL,
  `user_password` varchar(250) NOT NULL,
  `user_email` varchar(200) NOT NULL,
  `user_phone` int(13) NOT NULL,
  `user_type` text NOT NULL,
  `user_license` varchar(200) NOT NULL,
  `user_available_fl` tinyint(1) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `cr_user`
--

INSERT INTO `cr_user` (`user_id`, `user_firstname`, `user_lastname`, `user_password`, `user_email`, `user_phone`, `user_type`, `user_license`, `user_available_fl`) VALUES
(1, 'Shruti', 'Bidada', '$2y$10$MaRIPoW2fM5hbKP4FPQ2S.726tEWWRY5PGrAAKEQSN1sqEu/ByX52', 'shrutz19@gmail.com', 2147483647, 'customer', 'fdgfghrthth', 0),
(2, 'Ashish', 'Mohapatra', '$2y$10$2zCN.RtWmp7d8v3W5IXFF.6TyT6b4FLNBnh1rYFWee69DD7nDnaNi', 'admin@digiashish.com', 2147483647, 'admin', 'sdfghj45678fgh', 0),
(4, 'Vidya ', 'Mani', '$2y$10$2zCN.RtWmp7d8v3W5IXFF.6TyT6b4FLNBnh1rYFWee69DD7nDnaNi', 'sm.vidya@gmail.com', 2147483647, 'admin', 'qwert12345', 0),
(5, 'Vidya ', 'Mani1', '$2y$10$167PK3G/0GOcm1WypP.IXuJcYqL5lWYFl1zVp8MN7TaJI2CMjU73O', 'vidya@gmail.com', 2147483647, 'customer', 'qwert123451', 0),
(6, 'root', 'root', '$2y$10$hQJKgNajVBqM3RS3Ovd2n.On7.enAMS1SVO3663sOYLGs1tzOionO', 'root@root.com', 2147483647, 'customer', '123abc123', 0),
(7, 'test1', 'test1', '$2y$10$yfe.NrrlWphEg2u2kc9PrO9Zk7caVV.J7kgbjYKJpYqJMeVLtDNzu', 'test1@gmail.com', 2147483647, 'customer', '1231233xyz', 0),
(8, 'test2', 'test2', '$2y$10$gZ23vfL2g3xwxNucHENUhOrsxJHj6gajXlNOto.Vof5GzeLN.3Wom', 'test2@gmail.com', 2147483647, 'customer', '123412345667789', 0);

--
-- Indexes for dumped tables
--

--
-- Indexes for table `cr_booking`
--
ALTER TABLE `cr_booking`
  ADD PRIMARY KEY (`booking_id`),
  ADD KEY `booking_user_fk` (`user_id`);

--
-- Indexes for table `cr_car`
--
ALTER TABLE `cr_car`
  ADD PRIMARY KEY (`car_no`),
  ADD KEY `car_color_fk` (`color_id`),
  ADD KEY `car_mfg_fk` (`mfg_id`);

--
-- Indexes for table `cr_car_location`
--
ALTER TABLE `cr_car_location`
  ADD PRIMARY KEY (`location_zip`,`car_no`),
  ADD KEY `car_location_fk` (`car_no`);

--
-- Indexes for table `cr_color`
--
ALTER TABLE `cr_color`
  ADD PRIMARY KEY (`color_id`);

--
-- Indexes for table `cr_locations`
--
ALTER TABLE `cr_locations`
  ADD PRIMARY KEY (`location_zip`);

--
-- Indexes for table `cr_mfg`
--
ALTER TABLE `cr_mfg`
  ADD PRIMARY KEY (`mfg_id`),
  ADD KEY `mfg_size_fk` (`size_id`);

--
-- Indexes for table `cr_payment`
--
ALTER TABLE `cr_payment`
  ADD PRIMARY KEY (`payment_id`),
  ADD KEY `payment_booking_fk` (`booking_id`);

--
-- Indexes for table `cr_size`
--
ALTER TABLE `cr_size`
  ADD PRIMARY KEY (`size_id`);

--
-- Indexes for table `cr_user`
--
ALTER TABLE `cr_user`
  ADD PRIMARY KEY (`user_id`),
  ADD UNIQUE KEY `user_license` (`user_license`),
  ADD UNIQUE KEY `user_email` (`user_email`);

--
-- AUTO_INCREMENT for dumped tables
--

--
-- AUTO_INCREMENT for table `cr_booking`
--
ALTER TABLE `cr_booking`
  MODIFY `booking_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=5;
--
-- AUTO_INCREMENT for table `cr_payment`
--
ALTER TABLE `cr_payment`
  MODIFY `payment_id` int(200) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=19;
--
-- AUTO_INCREMENT for table `cr_user`
--
ALTER TABLE `cr_user`
  MODIFY `user_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=9;
--
-- Constraints for dumped tables
--

--
-- Constraints for table `cr_booking`
--
ALTER TABLE `cr_booking`
  ADD CONSTRAINT `booking_user_fk` FOREIGN KEY (`user_id`) REFERENCES `cr_user` (`user_id`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- Constraints for table `cr_car`
--
ALTER TABLE `cr_car`
  ADD CONSTRAINT `car_color_fk` FOREIGN KEY (`color_id`) REFERENCES `cr_color` (`color_id`),
  ADD CONSTRAINT `car_mfg_fk` FOREIGN KEY (`mfg_id`) REFERENCES `cr_mfg` (`mfg_id`);

--
-- Constraints for table `cr_car_location`
--
ALTER TABLE `cr_car_location`
  ADD CONSTRAINT `car_location_fk` FOREIGN KEY (`car_no`) REFERENCES `cr_car` (`car_no`),
  ADD CONSTRAINT `zip_location_fk` FOREIGN KEY (`location_zip`) REFERENCES `cr_locations` (`location_zip`);

--
-- Constraints for table `cr_mfg`
--
ALTER TABLE `cr_mfg`
  ADD CONSTRAINT `mfg_size_fk` FOREIGN KEY (`size_id`) REFERENCES `cr_size` (`size_id`);
--
-- Constraints for table `cr_payment`
--
ALTER TABLE `cr_payment`
  ADD CONSTRAINT `payment_booking_fk` FOREIGN KEY (`booking_id`) REFERENCES `cr_booking` (`booking_id`) ON DELETE CASCADE ON UPDATE CASCADE;









##Languages used


The system was developed using php, Javascript and Ajax.
Bootstrap templates were used to design the front end structure of the system.


#The project can be accessed from the link below:

http://project.digiashish.com/


##Screenshots


The user is prompted to login to the system. The user can login either as a customer or admin. If a new user visits the site, the user can sign up as well.
LOGIN/SIGNUP

![Login/signup](ImageCaptures/Capture5.PNG?raw=true "Login")

An error message is displayed when invalid credentials are used.

After the user logs in, the customer is directed to the home page.

Home Page
![Login/signup](ImageCaptures/Capture.PNG?raw=true "Login")
![Login/signup](ImageCaptures/Capture2.PNG?raw=true "Login")


The system follows two filtering processes. The user has to select the duration of travel, along with the place of pickup location (Step 1).
The next filter is based on the type of car (step 2).
Based on the search criteria, the list of available cars is displayed in the system. The following screenshot shows that
List of Cars



The user can select the car, and proceed to checkout.



Validation is provided at this page. For instance, if the length of the card number is invalid.


If details entered are valid , then a successful booking is done.

The list of booking can been seen, from my account tab.










If the user logs in as an admin, then the following page is displayed. The user can delete a car, add a car or change the rate of a particular model.

If a car is deleted

If a car is added to a new location

If the rate is changed
