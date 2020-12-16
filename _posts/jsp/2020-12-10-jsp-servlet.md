---
layout: post
current: post
cover:  assets/built/images/jsp-logo.png
navigation: True
title: JSP 강좌(1) - JSP 기본
date: 2020-12-11 16:40:00
tags: [jsp]
class: post-template
subclass: 'post tag-jsp'
author: Jakezo
---

{% include jsp-table-of-contents.html %}

01_SERVLET/EX01/Ex02_servlet.java 설명

~~~java
package dao;

import java.sql.Connection;
import java.sql.Date;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.ArrayList;

import javax.naming.Context;
import javax.naming.InitialContext;
import javax.naming.NamingException;
import javax.sql.DataSource;

import dto.BlueDto;

public class BlueDao {
    private Connection con;
    private PreparedStatement ps;
    private ResultSet rs;
    private String sql;
    private Date regDate;

    // DataSource 객체가 제공하는 getConnection() 메소드를 사용한다

    // DataSource 객체 만들기
    private static DataSource dataSource;

    static { // 클래스 초기화를 위한 static 블록
    try{
    Context context = new InitialContext();
    dataSource = (DataSource)context.lookup("java:comp/env/jdbc/oracle");
    // Tomcat의 경우 java:comp/env/ 를 prefix로 사용한다.
    // Context.xml의 <Resource>태그의 name속성이 jdbc/oracle이다.
}catch(NamingException e){
    e.printStackTrace();
}
}

// Singleton pattern
// 하나의 인스턴스만 생성해서 사용하기 위해 패턴을 만들어줌
private BlueDao() {}
private static BlueDao blueDao = new BlueDao();
public static BlueDao getInstance() {// 인스턴스 없이 호출할 수 있도록 클래스 메소드로 만든다. (static)
    return blueDao;
}

/******* 1. 접속 종료 *******/
public void close(Connection con, PreparedStatement ps, ResultSet rs){
    try{
        if(rs != null) {rs.close();}
        if(ps != null) {ps.close();}
        if(con != null) {con.close();}
    }catch(Exception e){
        e.printStackTrace();
    }
}


}
~~~