# RecyclerView Project
---
- Create a useful example of recyclerView that displays at least 15 items, each item content of two text views. When click on any item will show Toast message that display id of clicked item.
> *Optional:* add an image in the item, thus the item has one image and two text views.
// main ---->>>>
package com.tuwaiq.rcvexample

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.Button
import androidx.recyclerview.widget.LinearLayoutManager
import androidx.recyclerview.widget.RecyclerView

class MainActivity : AppCompatActivity() {

    private lateinit var recycledView: RecyclerView
    private  var data: MutableList<User> = mutableListOf()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        recycledView = findViewById(R.id.rvRe)
        for (i in 1..50){
            val user = User(
                "fName $i" ,
                "lName $i",
            i)
            data += user
        }
        recycledView.layoutManager = LinearLayoutManager(this)
        recycledView.adapter = DataCollection(data)
    }
}


// activity_main -->>
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">


    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/rvRe"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</LinearLayout>

// User class -->>>>>
package com.tuwaiq.rcvexample

data class User (
val fName: String,
val lName: String,
val id: Int
)


//r_C_V.xml --->>>
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_margin="5dp">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="  ID: "/>
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/tvID"/>
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text=" Name: "/>
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/tvName"/>
    </LinearLayout>


</LinearLayout>



//DataCollection -->>>
package com.tuwaiq.rcvexample

import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.TextView
import android.widget.Toast
import androidx.recyclerview.widget.RecyclerView



class DataCollection(private val userList: List<User>): RecyclerView.Adapter<UserAdapter.ViewHolder>() {

        override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): UserAdapter.ViewHolder {
            val viewItem = LayoutInflater.from(parent.context)
                .inflate(R.layout.r_c_v, parent, false)
            return UserAdapter.ViewHolder(viewItem)
        }

        override fun onBindViewHolder(holder: UserAdapter.ViewHolder, position: Int) {
            val user = userList[position]
            holder.idTextView.text = user.id.toString()
            holder.nameTextView.text = "${user.fName} : ${user.lName}"

        }

        override fun getItemCount(): Int {
            return userList.size
        }
    }

    class UserAdapter{

        class ViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView), View.OnClickListener{
            val idTextView: TextView = itemView.findViewById(R.id.tvID)
            val nameTextView: TextView = itemView.findViewById(R.id.tvName)
            init {
                itemView.setOnClickListener(this)
            }
            override fun onClick(v: View?) {
                Toast.makeText(itemView.context, "${idTextView.text}", Toast.LENGTH_SHORT).show()
            }

        }

}