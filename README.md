# User Defined Functions (UDF) Library

To Contribute to the UDF Library 
1. Grab UDF template located here [udf_template.md](udf_template.md)
2. Add your UDF to (this document) ~/UDF/README.md
3. Add your UDF to the [Table of Contents](#table-of-contents)
4. Issue a pull request

## Table of Contents
* [String Based UDF](#string-based-udf)
  * [substring](#substring) - Given a string of text, return a substring from index begin to index end
  * [str_regex_match](#str_regex_match) - Given a string determine if regex matches, return a boolean
  * [string_to_string](#string_to_string) -  string_to_string
  * [str_len](#str_len) - Given a string count char to get string size
  * [str_find](#str_find) - Given a string find a string in a string, and return where it was found (-1 if not found)
  * [regex_filter_set](#regex_filter_set) - Given a set and regular expression filter out strings and return the set
  * [regex_filter_list](#regex_filter_list) - Given a list and regular expression filter out strings and return the list
  * [double_to_string](#double_to_string) - Given a double output a string
  * [int_to_string](#int_to_string) - Given a int output a string in regular format (not using scientific notation)
 * [Integer/Float Based UDF](#integerfloat-based-udf)
   * [str_to_int](#str_to_int) - Given a string of numbers convert into an int
   * [float_to_int](#float_to_int) - Given a float convert it into an int
   * [echo_int](#echo_int) - Given an int echo an int
* [Geo Based UDF](#geo-based-udf)
   * [getNearbyGridId](#getnearbygridid) - Given a distance in km and lat and lon return nearby
   * [geoDistance](#geodistance) - Given a a starting & ending lat and long calculate the distance
* [Random Generator UDF](#random-generator-udf)
   * [rand_int](#rand_int) - Given a min and max int generate a random integer from a uniform distribution between min and max
   * [rand_normal](#rand_normal) - Generate a random number from a standard normal distribution
   * [rand_uniform](#rand_uniform) - Generate a random number from a uniform distribution between 0 and 1
   * [rand_choice_from_map](#rand_choice_from_map) - Given a map with the key of each value representing the probability distribution, return a key randomly sampled from the map according to the probability distribution
   * [rand_choice_from_list](#rand_choice_from_list) - Given a list with the value of each index representing the probability distribution, return a index randomly sampled from the list according to the probability distribution
* [Vector Operator UDF](#vector-operator-udf)
   * [sum_ArrayAccum](#sum_ArrayAccum) - Given an array, return the sum of the elements
   * [diff_ArrayAccum_List](#diff_ArrayAccum_List) - Given two vectors, return a vector as the difference
   * [product_List_const](#product_List_const) - Given an vector (as a list) and a constant, return an vector as the product
   * [product_ArrayAccum_const](#sum_ArrayAccum) - Given an vector (as an array) and a constant, return an vector as the product
   * [product_Matrix_const](#product_Matrix_const) - Given an matrix and a constant, return an matrix as the product
   * [product_sparseVector_ArrayAccum](#product_sparseVector_ArrayAccum) - Given a sparse vector (as a map) and a vector (as an array), return the Hadamard product
   * [product_ArrayAccum_ArrayAccum](#product_ArrayAccum_ArrayAccum) - Given two vectors, return the Hadamard product
   * [product_Matrix_SparseVector](#product_Matrix_SparseVector) - Given a matrix and a sparse vector, return the product
   * [product_Matrix_Vector](#product_Matrix_Vector) - Given a matrix A and a vector x, return the product Ax
   * [product_Vector_Matrix](#product_Vector_Matrix) - Given a matrix A and a vector x, return the product x^TA
   * [dotProduct_ArrayAccum_List](#dotProduct_ArrayAccum_List) - Given a vector (as an array) and a vector (as a list), return the dot product
   * [dotProduct_List_List](#dotProduct_List_List) - Given two vectors (as two lists), return the dot product
   * [dotProduct_ArrayAccum_ArrayAccum](#dotProduct_ArrayAccum_ArrayAccum) - Given two vectors (as two arrays), return the dot product
   * [unit_ArrayAccum](#unit_ArrayAccum) - Given an interger n, generate a ones (as an array) of length n
   * [unit_List](#unit_List) - Given an interger n, generate a ones (as a list) of length n
* [Machine Learning UDF](#machine-learning-udf)
   * [softmax_ArrayAccum](#softmax_ArrayAccum) - Given a vector v (as an array), return softmax(v)
   * [ReLU_ArrayAccum](#ReLU_ArrayAccum) - Given a vector v (as an array), return ReLU(v)
   * [sigmoid_ArrayAccum](#sigmoid_ArrayAccum) - Given a vector v (as an array), return sigmoid(v)
   * [dropout_ArrayAccum](#dropout_ArrayAccum) - Given a vector v (as an array) and a dropout rate
   * [dropout_SparseVector](#dropout_SparseVector) - Given a spase vector v (as a map) and a dropout rate
   * [L2Norm_Matrix](#L2Norm_Matrix) - Given a matrix (as an array), return the L2 norm of the matrix
* [Others](#others)

## String Based UDF
### substring
Given a string of text, return a substring from index begin to index end

| Variable | Description| Example |
| -------- | -------- | -------- |
| str    | input string of text     | The Apple is Red   | 
| b    | index of string you would like to begin with     | index 4 = A     |
| e    |index of string you would like to end with    | index 8 = e|

**UDF Code**
```
inline string substring(string str, int b, int e) {
return str.substr (b,e);
}
```

**Example**
str = "The Apple is Red"
substring(s, 4, 8)

return = Apple

-----------

### str_regex_match
Given a string determine if regex matches, return a boolean


**UDF Code**
```
inline bool str_regex_match (string toCheck, string regEx) {
bool res = false;
// only performs the check when the input is valid
try {
  res = boost::regex_match(toCheck, boost::regex(regEx));
} catch (boost::regex_error err) {
  res = false;
}
return res;
}
```
**Example**
*Need to add*

-----------

### string_to_string
*Need to add*

**UDF Code**
```
  inline string to_string (double val) {
    char result[200];
    sprintf(result, "%g", val);
    return string(result);
  }
```
**Example**
*Need to add*

-----------

### str_len
Given a string count char to get string size

**UDF Code**
```
  inline int64_t str_len (string str) {
    return (int64_t) str.size();
  }
```
**Example**
*Need to add*

-----------

### str_find
Given a string find a string in a string, and return where it was found (-1 if not found)

**UDF Code**
```
 inline int64_t str_find (string str1, string str2) {
    return (int64_t) str2.find(str1);
  }
```
**Example**
*Need to add*

-----------

### regex_filter_set
Given a set and regular expression filter out strings and return the set

**UDF Code**
```
inline SetAccum <string> regex_filter_set (SetAccum <string>& inSet , string regEx) {
SetAccum <string> outSet;

for (auto& it :  inSet.data_) {
  if (str_regex_match(it, regEx)) {
    outSet += it;
  }
}
return outSet;
}
```
**Example**

```
CREATE QUERY tryFilterBag(string regex) FOR GRAPH MyGraph { 
  /* Write query logic here */ 
	ListAccum <STRING> @outList ;
	SetAccum <STRING> @outSet;
	
	bv = {BagVertex.*}; 
	
	bv = select bvv from bv:bvv
	POST-ACCUM 
	  bvv.@outList = regex_filter_list(bvv.myList, regex),
	  bvv.@outSet = regex_filter_set(bvv.mySet, regex);
      //HAVING bvv.@outList.size() > 0; // uncomment for direct filtration
	  
	cv = select cvv from bv:cvv
	WHERE cvv.@outList.size() > 0 AND cvv.@outSet.size() > 0;

  PRINT bv, cv; 
}
```

### regex_filter_list
Given a list and regular expression filter out strings and return the list 

**UDF Code**
```
inline ListAccum <string> regex_filter_list (ListAccum <string>& inBag , string regEx) {
ListAccum <string> outBag;

for (int i=0; i < inBag.size(); i++){
    if (str_regex_match(inBag.get(i), regEx)) {
        outBag += inBag.get(i);
    }
}
return outBag;
}
```
**Example**
```
CREATE QUERY tryFilterBag(string regex) FOR GRAPH MyGraph { 
  /* Write query logic here */ 
	ListAccum <STRING> @outList ;
	SetAccum <STRING> @outSet;
	
	bv = {BagVertex.*}; 
	
	bv = select bvv from bv:bvv
	POST-ACCUM 
	  bvv.@outList = regex_filter_list(bvv.myList, regex),
	  bvv.@outSet = regex_filter_set(bvv.mySet, regex);
      //HAVING bvv.@outList.size() > 0; // uncomment for direct filtration
	  
	cv = select cvv from bv:cvv
	WHERE cvv.@outList.size() > 0 AND cvv.@outSet.size() > 0;

  PRINT bv, cv; 
}
```
### double_to_string
Given a double output a string

**UDF Code**
```
  inline string bigint_to_string (double val) {
    char result[200];
    sprintf(result, "%.0f", val);
    return string(result);
  }
```
**Example**
*Need to add*

-----------

### int_to_string
Given a int output a string in regular format (not using scientific notation)

**UDF Code**
```
  inline string int_to_string (uint64_t val) {
    char result[200];
    sprintf(result, "%u", val);
    return string(result);
  }
```
**Example**
*Need to add*

-----------

## Integer/Float Based UDF

### echo_int
Given an int echo an int

**UDF Code**
```
  inline int64_t echo_int (int64_t echoThis) {
      return (int64_t) echoThis;
  }
```
**Example**
*Need to add*

-----------

### str_to_int
Given a string of numbers convert into an int

**UDF Code**
```
  inline int64_t str_to_int (string str) {
    return atoll(str.c_str());
  }
```
**Example**
*Need to add*

-----------

### float_to_int
Given a float convert it into an int

**UDF Code**
```
  inline int64_t float_to_int (float val) {
    return (int64_t) val;
  }
```
**Example**
*Need to add*

-----------

## Geo Based UDF

### getNearbyGridId
Given a distance in km and lat and lon return nearby

**UDF Code**
```
inline SetAccum<string> getNearbyGridId (double distKm, double lat, double lon) {

    string gridIdStr = map_lat_long_grid_id(lat, lon); 
    uint64_t gridId = atoi(gridIdStr.c_str());

    int dia_long = gridNumLong (distKm, lat);
    int dia_lat = gridNumlat (distKm);

    int minus_dia_long = -1*dia_long;
    int minus_dia_lat  = -1*dia_lat;

    SetAccum<string> result;

    result += gridIdStr;

    int origin_lat = gridId/NUM_OF_COLS;
    int origin_lon = gridId%NUM_OF_COLS;

    for(int i = minus_dia_lat; i <= dia_lat; i++) {
      for(int j = minus_dia_long; j <= dia_long; j++) {
        int new_lat = origin_lat + i;
        int new_lon = origin_lon + j;

        // wrap around
        if (new_lat < 0) {
          new_lat = NUM_OF_ROWS + new_lat;
        } else if (new_lat > NUM_OF_ROWS) {
          new_lat = new_lat - NUM_OF_ROWS;
        }

        if (new_lon < 0) {
          new_lon = NUM_OF_COLS + new_lon;
        } else if (new_lon > NUM_OF_COLS) {
          new_lon = new_lon - NUM_OF_COLS;
        }

        int id = new_lon + NUM_OF_COLS * new_lat;

        result += std::to_string(id);
      }
    }
    return result;
  }
  ```
**Example**
*Need to add*

-----------

### geoDistance
Given a a starting & ending lat and long calculate the distance

**UDF Code**
```
  inline double geoDistance(double latitude_from, double longitude_from, double latitude_to, double longitude_to) {
    double phi_1 = deg2rad(latitude_from);
    double lambda_1 = deg2rad(longitude_from);
    double phi_2 = deg2rad(latitude_to);
    double lambda_2 = deg2rad(longitude_to);
    double u = sin(phi_2 - phi_1)/2.0;
    double v = sin(lambda_2 - lambda_1)/2.0;
    return 2.0 * earthRadiusKm * asin(sqrt(u * u + cos(phi_1) * cos(phi_2) * v * v));
  }
```
**Example**
*Need to add*

-----------

## Random Generator UDF

### rand_int
Given a min and max int generate a random integer 

**UDF Code**
```
inline int64_t rand_int (int minVal, int maxVal) {
  std::random_device rd;
  std::mt19937 e1(rd());
  std::uniform_int_distribution<int> dist(minVal, maxVal);
  return (int64_t) dist(e1);

}
```

**Example**
*Need to add*

-----------

### rand_normal
Generate a random number from a standard normal distribution 

**UDF Code**
```
  inline double rand_normal () {
      unsigned seed = std::chrono::system_clock::now().time_since_epoch().count();
      std::default_random_engine generator(seed);
      std::normal_distribution<double> distribution(0,1);
      double y = distribution(generator);
      return y;
  }
```

**Example**
*Need to add*

-----------

### rand_uniform
Generate a random number from a uniform distribution between 0 and 1

**UDF Code**
```
  inline double rand_uniform () {
      unsigned seed = std::chrono::system_clock::now().time_since_epoch().count();
      srand(seed);
      double y = ((double) rand() / (RAND_MAX));
      return y;
  }
```

**Example**
*Need to add*

-----------

### rand_choice_from_map
Given a map with the key of each value representing the probability distribution, return a key randomly sampled from the map according to the probability distribution 

**UDF Code** (need to be optimized)
```
  inline int64_t rand_choice_from_map (MapAccum<int64_t, double>& Prob_Map) {
      std::vector<double> y_prob;
      std::vector<int64_t> y_id;
      for (auto yp : Prob_Map){
        y_id.push_back(yp.first);
        y_prob.push_back(yp.second);
      }
      unsigned seed = std::chrono::system_clock::now().time_since_epoch().count();
      std::default_random_engine generator(seed);
      std::discrete_distribution<int> distribution(y_prob.begin(),y_prob.end());
      int id = distribution(generator);
      return y_id[id];
  }
```

**Example**
*Need to add*

-----------

### rand_choice_from_list
Given a list with the value of each index representing the probability distribution, return a index randomly sampled from the list according to the probability distribution

**UDF Code**
```
  inline int rand_choice_from_list(ListAccum<float>& p){
    std::vector<float> a = p.data_;
    unsigned seed = std::chrono::system_clock::now().time_since_epoch().count();
    std::default_random_engine gen(seed);
    std::discrete_distribution<> dis(a.begin(), a.end());
    return dis(gen);
  }
```

**Example**
*Need to add*

-----------

## Vector Operator UDF

### dotProduct_ArrayAccum_ArrayAccum
Given two vectors (as two arrays), return the dot product 

**UDF Code**
```
  inline double dotProduct_ArrayAccum_ArrayAccum (ArrayAccum<SumAccum<double>>& aArray, ArrayAccum<SumAccum<double>>& bArray) {
      double c = 0;
      for (uint32_t i=0; i < aArray.data_.size(); i++){
        c += bArray.data_[i]*aArray.data_[i];
    }
      return c;
  }
```

**Example**
*Need to add*

-----------

## Machine Learning UDF

### softmax_ArrayAccum
Given a vector v (as an array), return softmax(v) 

**UDF Code**
```
  inline ArrayAccum<SumAccum<double>> softmax_ArrayAccum (ArrayAccum<SumAccum<double>>& xArray) {
      ArrayAccum<SumAccum<double>> yArray(xArray.dim_);
      std::vector<SumAccum<double>>& data = yArray.data_;
      double sum = 0;
      for (uint32_t i=0; i < xArray.data_.size(); i++){
          yArray.data_[i] = exp(xArray.data_[i]);
          sum += yArray.data_[i];
      }
      for (uint32_t i=0; i < xArray.data_.size(); i++){
          yArray.data_[i] = yArray.data_[i]/sum;
      }
      return yArray;
  }
```

**Example**
*Need to add*

-----------

### ReLU_ArrayAccum 
Given a vector v (as an array), return ReLU(v)

**UDF Code**
```
  inline ArrayAccum<SumAccum<double>> ReLU_ArrayAccum (ArrayAccum<SumAccum<double>>& xArray) {
      ArrayAccum<SumAccum<double>> yArray(xArray.dim_);
      std::vector<SumAccum<double>>& data = yArray.data_;
      for (uint32_t i=0; i < xArray.data_.size(); i++){
          if (xArray.data_[i] > 0){
              yArray.data_[i] = xArray.data_[i];
          } else{
              yArray.data_[i] = 0;
          }
      }
      return yArray;
  }
```

**Example**
*Need to add*

-----------

### sigmoid_ArrayAccum 
Given a vector v (as an array), return sigmoid(v)

**UDF Code**
```
  inline ArrayAccum<SumAccum<double>> sigmoid_ArrayAccum (ArrayAccum<SumAccum<double>>& xArray) {
      ArrayAccum<SumAccum<double>> yArray(xArray.dim_);
      std::vector<SumAccum<double>>& data = yArray.data_;
      for (uint32_t i=0; i < xArray.data_.size(); i++){
        yArray.data_[i] = 1/(1+exp(-xArray.data_[i]))-xArray.data_[i];
    }
      return yArray;
  }
```

**Example**
*Need to add*

-----------

### dropout_ArrayAccum 
Given a vector v (as an array) and a dropout rate

**UDF Code**
```
  inline ArrayAccum<SumAccum<double>> dropout_ArrayAccum (ArrayAccum<SumAccum<double>>& xArray, double p) {
      unsigned seed = std::chrono::system_clock::now().time_since_epoch().count();
      srand(seed);
      ArrayAccum<SumAccum<double>> yArray(xArray.dim_);
      std::vector<SumAccum<double>>& data = yArray.data_;
      for (uint32_t i=0; i < xArray.data_.size(); i++){
        if (((double) rand() / (RAND_MAX)) < p){
              yArray.data_[i] = xArray.data_[i]/p;
        }
    }
      return yArray;
  }
```

**Example**
*Need to add*

-----------

### dropout_SparseVector 
Given a spase vector v (as a map) and a dropout rate

**UDF Code**
```
  inline MapAccum<int64_t,double> dropout_SparseVector (MapAccum<int64_t,double>& x, double p) {
      MapAccum<int64_t,double> y;
      unsigned seed = std::chrono::system_clock::now().time_since_epoch().count();
      srand(seed);
      for (auto it = x.data_.begin(); it != x.data_.end(); ++it) {
          if (((double) rand() / (RAND_MAX)) < p){
              y.data_[it->first] += (it->second)/p;
          }
      }
      return y;
  }
```

**Example**
*Need to add*

-----------

### L2Norm_Matrix 
Given a matrix (as an array), return the L2 norm of the matrix

**UDF Code**
```
  inline double L2Norm_Matrix (const ArrayAccum<SumAccum<double>>& M) {
      double c = 0;
      for (uint32_t i=0; i < M.data_.size(); i++){
        c += M.data_[i]*M.data_[i];
    }
      return c;
  }
```

**Example**
*Need to add*

## Others

### getHH 
Get the VERTEX hh in a tuple

**UDF Code**
```
  template <typename tuple>
  inline VERTEX getHH (tuple tup) {
    return tup.hh;
  }
```
