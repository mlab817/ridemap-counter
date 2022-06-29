# RIDEMAP: Passenger Count through Manual Passenger Counting

## Description

This mobile app allows registered smartphones to collect data
on number of passengers boarding and leaving vehicles in the 
different stations of EDSA Busway.

## Requirements

1. [Free Expo account](https://expo.dev/signup)
2. React Native and Expo for mobile app development
3. Smartphones with internet

The [Laravel backend for the Ridemap](https://github.com/mlab817/ridemap-php)
already supports this app. The endpoint for submission of face detection is `/api/passenger-count`. 
The backend accepts a single input with the following attributes: `station_id`,
`passenger_in`, `passenger_out`, and `scanned_at`. `user_id` is extracted from 
the token used to authenticate the device.

## Building the App

Since this app has been created with [expo](expo.dev),
the app can also be built with it through the
[Expo Application Services](https://docs.expo.dev/eas/).
To do this make sure that `eas-cli` is installed in your
computer with `npm i -g eas-cli`. Then, in your app's root
directory, just run `eas build` and follow the instruction.
You can view the progress in [expo.dev](https://expo.dev/) 
website, i.e. dashboard. Afterwards, you can download the 
app bundle which you can distribute to users or submit to
app / play store.

__Important__: Do not forget to update the api configuration in the
`utils.js` file to point to the url of the API of the backend. Specifically,
this line:

```javascript
export const api = axios.create({
   baseURL: 'https://ridemap-php.herokuapp.com/api'
})
```

## Workflow

### Device Authentication

To use this app, devices must be registered in the server. To do
this, follow the instructions below:

1. Download the app
2. Open the app to connect to the server for the first time
3. The app will show an invalid device message along with the device ID.
Use this device ID to register the device in the server.

`
Note: The device ID does not refer to the actual device ID of the
device but rather the device ID of the app tied to the server. This
is unique for every app that is installed in the device.`

Read more here: [Android](https://docs.expo.dev/versions/v45.0.0/sdk/application/#applicationandroidid)
and [iOS](https://docs.expo.dev/versions/v45.0.0/sdk/application/#applicationgetiosidforvendorasync)

## Getting Started

Install the necessary tools:

1. Any IDE (Webstorm is preferred but you can also use Atom and VS Code)
2. Install Nodejs
3. Install Expo
4. Install Expo Go in IOS/Android
5. Install Git

Follow the following steps to get set up:

1. Clone this repository

```console
git clone https://github.com/mlab817/ridemap-counter.git
```

2. Change directory to ridemap-counter

```console
cd ridemap-counter
```

3. Install dependencies


```console
npm install
```

4. Update the API endpoint in utils.js file

```javascript
export const api = axios.create({
   baseURL: 'https://ridemap-php.herokuapp.com/api'
})
```

5. Start expo dev server


```console
expo start
```

Or

```console
expo r -c
```

The second command is used when you cannot connect your device to the webserver. 

Follow the instructions in the CLI message to connect your simulator or physical device.

## Building and Distributing the App

To build the app, install the Expo Application Services.

1. Create a free account in [Expo](https://expo.dev).
2. Install eas-cli to use eas in command prompt and/or terminal.

```console
npm i -g eas-cli
```

3. From the root directory, run:

```console
eas build
```

Follow the on-screen instructions. You will find the android/ios bundles in your Expo account under Build menu, e.g. https://expo.dev/accounts/{accountName}/projects/ridemap-counter/builds. You may also integrate submission to Play Store
and App Store.

> Note: Unfortunately, to build IOS applications, you will need to apply and register to Apple Developer Program which 
> costs $99 yearly. Android build is free and can be downloaded for distribution.

### Using the App

1. Open app
2. Device connects to server
3. Server verifies that device is registered
   1. If device is not registered, display invalid device message along with the device ID. Note that the device ID is not the actual device ID but rather the ID of the device tied with the app.
   2. If device is registered, proceed
4. Prompt user to select station where it is located
5. Input passenger in and out
6. Press submit

After succesful submission, the form will be reset and the user can immediately input the next passenger count. 

## Table Structure

### - users

Stores data of users of the system

| Attribute | Type      | Description                                            |
|-----------|-----------|--------------------------------------------------------|
| id        | int autoincrement  | Primary key of the table |
| name      | varchar   | Name of the user                 |
| email     | varchar   | Email of the user               |
| email_verified_at     | timestamp   | Timestamp when the user validated their email              |
| password  | varchar   | Hashed password of the user     |
| device_id | varchar   | Device ID of the user               | |
| created_at| timestamp | Timestamp when the record was saved in the database    |
| updated_at| timestamp | Timestamp when the record was updated in the database  |

### - stations

Stores data of stations in EDSA Busway

| Attribute | Type               | Description              |
|-----------|--------------------|--------------------------|
| id        | int autoincrement  | Primary key of the table |
| name      | varchar            | Name of the station      |
| created_at| timestamp | Timestamp when the record was saved in the database    |
| updated_at| timestamp | Timestamp when the record was updated in the database  |

### - passenger_counts

Stores data on scanned QR codes

| Attribute | Type      | Description                                            |
|-----------|-----------|--------------------------------------------------------|
| id        | int autoincrement | Primary key of the table                 |
| station_id| int       | Foreign key referencing stations table            |
| passenger_in| int   | Count of passengers entering the vehicle            |
| passenger_out| int   | Count of passengers leaving the vehicle            |
| scanned_at| timestamp | Timestamp when the entry was generated |
| user_id   | int       | Foreign key referencing users table (user that submitted the data)   |
| created_at| timestamp | Timestamp when the record was saved in the database    |
| updated_at| timestamp | Timestamp when the record was updated in the database  |

## Screenshots

| ![Splashscreen](https://user-images.githubusercontent.com/29625844/176327396-36fa6458-4159-45b8-a6c7-462034a26ebf.png) | ![Device ID](https://user-images.githubusercontent.com/29625844/176327425-75f8868a-263d-44ec-9ccf-514c5ccea8f7.png) |
|:------------------:|:-----------------:|
| ![Select Station](https://user-images.githubusercontent.com/29625844/176327449-37a9db0f-d31e-4f2b-8666-eebf7fcce0b9.png) | ![Input Data](https://user-images.githubusercontent.com/29625844/176327415-abeff8c0-489c-4a2c-97dc-28b0aa6ca755.png) |

1. Screen 1 - Splash screen
2. Screen 2 - QR Code for the Device ID which can be scanned to easily copy the device ID
3. Screen 3 - Select station where device is located
4. Screen 4 - Input data on passenger entering vehicles and leaving vehicles and submit

## Author

This mobile app is developed by [Mark Lester Bolotaolo](https://github.com/mlab817).
