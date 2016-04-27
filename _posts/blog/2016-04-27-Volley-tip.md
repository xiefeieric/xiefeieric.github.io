---
layout: post
title: Android Volley Framework - 3 ways to submit POST
description: Sample code to demostrate how to POST by Volley
category: blog
---

**1**. Normal POST, server send string back.     

~~~java
RequestQueue requestQueue = Volley.newRequestQueue(getApplicationContext());

StringRequest stringRequest = new StringRequest(Request.Method.POST,httpurl,
    new Response.Listener<String>() {
        @Override
        public void onResponse(String response) {
            Log.d(TAG, "response -> " + response);
        }
    }, new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            Log.e(TAG, error.getMessage(), error);
        }
    }) {
    @Override
    protected Map<String, String> getParams() {
        //在这里设置需要post的参数
            Map<String, String> map = new HashMap<String, String>();  
            map.put("name1", "value1");  
            map.put("name2", "value2");  

          return params;
    }
};        

requestQueue.add(stringRequest);
~~~

**2**. JSON way to submit POST, server send JSON string back. 

~~~java
RequestQueue requestQueue = Volley.newRequestQueue(getApplicationContext());

Map<String, String> map = new HashMap<String, String>();  
map.put("name1", "value1");  
map.put("name2", "value2");  

JSONObject jsonObject = new JSONObject(params);
JsonRequest<JSONObject> jsonRequest = new JsonObjectRequest(Method.POST,httpurl, jsonObject,
    new Response.Listener<JSONObject>() {
        @Override
        public void onResponse(JSONObject response) {
            Log.d(TAG, "response -> " + response.toString());

        }
    }, new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            Log.e(TAG, error.getMessage(), error);
    }
    })
    {
    //注意此处override的getParams()方法,在此处设置post需要提交的参数根本不起作用
    //必须象上面那样,构成JSONObject当做实参传入JsonObjectRequest对象里
    //所以这个方法在此处是不需要的
//    @Override
//    protected Map<String, String> getParams() {                
//          Map<String, String> map = new HashMap<String, String>();  
//            map.put("name1", "value1");  
//            map.put("name2", "value2");  
                
//        return params;
//    }
            
    @Override
    public Map<String, String> getHeaders() {
        HashMap<String, String> headers = new HashMap<String, String>();
        headers.put("Accept", "application/json");
        headers.put("Content-Type", "application/json; charset=UTF-8");
                
        return headers;
    }
};
requestQueue.add(jsonRequest);
~~~

**3**. Normal way to submit POST, server send JSON string back.

~~~java
RequestQueue requestQueue = Volley.newRequestQueue(getApplicationContext());

Map<String, String> map = new HashMap<String, String>();  
map.put("name1", "value1");  
map.put("name2", "value2");  

JSONObject jsonObject = new JSONObject(params);
JsonRequest<JSONObject> jsonRequest = new JsonObjectRequest(Method.POST,httpurl, jsonObject,
    new Response.Listener<JSONObject>() {
        @Override
        public void onResponse(JSONObject response) {
            Log.d(TAG, "response -> " + response.toString());

        }
    }, new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            Log.e(TAG, error.getMessage(), error);
    }
    })
    {
    //注意此处override的getParams()方法,在此处设置post需要提交的参数根本不起作用
    //必须象上面那样,构成JSONObject当做实参传入JsonObjectRequest对象里
    //所以这个方法在此处是不需要的
//    @Override
//    protected Map<String, String> getParams() {                
//          Map<String, String> map = new HashMap<String, String>();  
//            map.put("name1", "value1");  
//            map.put("name2", "value2");  
                
//        return params;
//    }
            
    @Override
    public Map<String, String> getHeaders() {
        HashMap<String, String> headers = new HashMap<String, String>();
        headers.put("Accept", "application/json");
        headers.put("Content-Type", "application/json; charset=UTF-8");
                
        return headers;
    }
};
requestQueue.add(jsonRequest);
~~~

Then create a new RequestQueue, and put request into the queue.

~~~
RequestQueue requestQueue = Volley.newRequestQueue(getApplicationContext());

Request<JSONObject> request = new NormalPostRequest(httpurl,
    new Response.Listener<JSONObject>() {
        @Override
        public void onResponse(JSONObject response) {
            Log.d(TAG, "response -> " + response.toString());
        }
    }, new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            Log.e(TAG, error.getMessage(), error);
        }
    }, params);

requestQueue.add(request);
~~~

You can find more detail from [Google Volley].

[Google Volley]: http://developer.android.com/training/volley/index.html




