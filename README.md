# Nomad Homes XML feed specification

This specification outlines requirements for XML feed, expected data and data types.

## Requirements

### XML document

* *`MUST`* be valid XML file
* *`MUST`* be in UTF-8 encoding
* *`MUST`* use [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) for all date- and time-related data
* *`MUST`* use UTC timezone for all time-related data
* *`MUST`* include available listings only

### Types

Reference [W3C XML Schema Definition Language](https://www.w3.org/TR/xmlschema11-2/)

### Elements

#### listings

```xml
<listings updated_at="2020-08-30T09:30:10Z">
</listings>
```

#### listing

```xml
<listings updated_at="2020-08-30T09:30:10Z">
  <listing>
    <reference_number>NH-R-3459</reference_number>
    <price currency="AED">1200000.00</price>
    <property_type>villa</property_type>
    <property_status>completed</property_status>
    <offering_type>sale</offering_type>
    <size units="sqft">2500</size>
    <bedrooms>4</bedrooms>
    <bathrooms>5</bathrooms>
    <furnished>furnished</furnished>
    <parking_spots>1</parking_spots>
    <description><![CDATA[Detailed description]]></description>
    <amenities>
      <amenity><![CDATA[Balcony]]></amenity>
      <amenity><![CDATA[Pool]]></amenity>
      <amenity><![CDATA[Pets Allowed]]></amenity>
    </amenities>
    <views>
      <view><![CDATA[Pool]]></view>
      <view><![CDATA[Sea]]></view>
    </views>
    <images>
      <image><![CDATA[https://your-domain.com/image_1.jpg]]></image>
      <image><![CDATA[https://your-domain.com/image_2.jpg]]></image>
    </images>
    <city><![CDATA[Dubai]]></city>
    <community><![CDATA[Reem]]></community>
    <sub_community><![CDATA[Mira Oasis]]></sub_community>
    <tower><![CDATA[Mira Oasis 2]]></tower>
    <floor_number>2</floor_number>
    <unit_number>21A</unit_number>
    <latitude>25.01658988</latitude>
    <longitude>55.29835291</longitude>
    <agent>
      <name><![CDATA[John Doe]]></name>
      <email>john@doe-properties.com</email>
      <phone>971-55-555-5555</phone>
    </agent>
    <created_at>2020-08-30T09:29:10Z</created_at>
    <updated_at>2020-08-30T09:30:10Z</updated_at>
  </listing>
</listings>
```

| Element | Type | Description | Example Value |
| --- | --- | --- | --- |
| reference_number | `token` | **`REQUIRED`** **`UNIQUE`** Unique listing reference number. | `NH-R-3459` |
| price | `decimal` | **`REQUIRED`** Price of the property and currency. | `1200000.00` |
| property_type | `token` | **`REQUIRED`** Type of the property. Accepted values: `apartment`, `villa`, `penthouse`, `duplex`, `townhouse`. | `villa` |
| property_status | `token` | **`REQUIRED`** Status of the property. Accepted values: `completed`, `off_plan`. | `off_plan` |
| offering_type | `token` | **`REQUIRED`** Type of the offering. Accepted values: `rent`, `sale`. | `sale` |
| size | `positiveInteger` | **`REQUIRED`** Floor area size. | `2500` |
| bedrooms | `integer` | **`REQUIRED`** Number of bedrooms. `0` or `0.5` for studio. | `4` |
| bathrooms | `decimal` | **`REQUIRED`** Number of bathrooms, can include half size bathroom defined as half decimal, e.g. `2.5` which means 2 full bathrooms and a half bathroom. | `5.0` |
| furnished | `token` | **`REQUIRED`** Accepted values: `furnished`, `unfurnished`. | `furnished` |
| parking_spots | `integer` | A number from 0 and up. | `1` |
| description | `string` | Detailed description. Enclosed in `CDATA`. | `<![CDATA[description]]>` |
| amenities | element with nodes | **`REQUIRED`** List of amenities as an array. ||
| views | element with nodes | **`REQUIRED`** List of views as an array. ||
| images | element with nodes | **`REQUIRED`** List of **non-watermarked** images as an array. ||
| city | `string` | **`REQUIRED`** City where property is located. Enclosed in `CDATA`. | `<![CDATA[Dubai]]>` |
| community | `string` | **`REQUIRED`** Community where property is located. Enclosed in `CDATA`. | `<![CDATA[Reem]]>` |
| sub_community | `string` | Sub-community where property is located. Enclosed in `CDATA`. | `<![CDATA[Mira Oasis]]>` |
| tower | `string` | **`REQUIRED`** Tower where property is located. Enclosed in `CDATA`. | `<![CDATA[Mira Oasis 2]]>` |
| floor_number | `integer` | Floor number. | `2` |
| unit_number | `string` | Unit number of the property. | `21A` |
| latitude | `decimal` | Property location latitude. | `25.01658988` |
| longitude | `decimal` | Property location longitude. | `55.29835291` |
| agent | element with nodes | **`REQUIRED`** Agent contact information. ||
| created_at | `dateTime` | **`REQUIRED`** Timestamp of the listing creation. | `2020-08-30T09:29:10Z` |
| updated_at | `dateTime` | **`REQUIRED`** Timestamp of the last listing update. | `2020-08-30T09:30:10Z` |

#### amenities

| Element | Type | Description | Example Value |
| --- | --- | --- | --- |
| amenity | `normalizedString` | Amenity name. Enclosed in `CDATA`. Full list of supported amenities is included below. |`<![CDATA[Balcony]]>`|

**Supported amenities**

* Balcony
* Barbecue Area
* Built in Wardrobes
* Built-in Wardrobes
* Children's Play Area
* Community Gym
* Community Pool
* Community Spa
* Concierge
* Covered Parking
* Gym
* Kitchen Appliances
* Maid Service
* Pets Allowed
* Pool
* Private Garden
* Private Jacuzzi
* Private Pool
* Security
* Shared Gym
* Shared Pool
* Study
* Walk-in Closet

#### views

| Element | Type | Description | Example Value |
| --- | --- | --- | --- |
| view | `normalizedString` | View name. Enclosed in `CDATA`. Full list of supported views is included below. | `<![CDATA[Garden]]>` |

**Supported views**

* Atlantis
* Burj Al Arab
* Burj Khalifa
* Canal/Water
* City/Community
* Fountain
* Garden
* Golf
* Lake
* Landmark
* Marina
* Park
* Pool
* Sea
* Sheikh Zayed Road
* The Frame
* The Palm

#### images

| Element | Type | Description | Example Value |
| --- | --- | --- | --- |
| image | `anyURI` | Non-watermarked image URL. Enclosed in `CDATA`. | `<![CDATA[https://your-domain.com/image_1.jpg]]>` |

#### agent

| Element | Type | Description | Example Value |
| --- | --- | --- | --- |
| name | `token` | **`REQUIRED`** Agent name. Enclosed in `CDATA`. | `<![CDATA[John Doe]]>` |
| email | `token` | **`REQUIRED`** Agent email. | `john@doe-properties.com` |
| phone | `token` | **`REQUIRED`** Agent phone. | `971-55-555-5555` |

### Attributes

| Element | Attribute | Type | Description | Example |
| --- | --- | --- | --- | --- |
| listings | updated_at | `dateTime` | **`REQUIRED`** Timestamp of the last update for the document. | `2020-08-30T09:30:10Z` |
| listing | price | `token` | **`REQUIRED`** Currency code in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format. | `AED` |
| listing | units | `token` | **`REQUIRED`** Floor area size measurement units. Accepted values: `sqft`, `sqm`. | `sqft` |

