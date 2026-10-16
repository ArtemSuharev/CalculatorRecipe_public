package com.artemsuharev.timbu.myapplicationnew.cr_fragments.updateText

import android.annotation.SuppressLint
import android.app.Dialog
import android.os.Bundle
import android.view.LayoutInflater
import android.view.ViewGroup
import android.widget.LinearLayout
import android.widget.TextView
import android.widget.Toast
import androidx.fragment.app.DialogFragment
import com.artemsuharev.timbu.myapplicationnew.R
import com.artemsuharev.timbu.myapplicationnew.cr_fragments.helpers.setOnSafeClickListener

class UpdatesDialogFragment : DialogFragment() {

    private val repository by lazy { UpdatesRepository(requireContext()) }

    @SuppressLint("UseGetLayoutInflater", "MissingInflatedId")
    override fun onCreateDialog(savedInstanceState: Bundle?): Dialog {

        val dialog = Dialog(requireContext())
        dialog.setContentView(R.layout.f_dialog_updates)

        val container = dialog.findViewById<LinearLayout>(R.id.updatesContainer)
        val unreadUpdates = repository.getUnreadUpdates()

        // Кнопка закрытия
        val buttonClose = dialog.findViewById<TextView>(R.id.close)
        buttonClose.setOnSafeClickListener {
            unreadUpdates.forEach { repository.markAsRead(it.id) }
            dialog.dismiss()
        }

        if (unreadUpdates.isEmpty()) {
            Toast.makeText(requireContext(), "Всё прочитано", Toast.LENGTH_SHORT).show()
            dialog.dismiss()
            return dialog
        }

        unreadUpdates.forEach { update ->
            val itemView = LayoutInflater.from(requireContext())
                .inflate(R.layout.f_item_update, container, false)

            itemView.findViewById<TextView>(R.id.title).text = update.title
            itemView.findViewById<TextView>(R.id.description).text = update.description

            itemView.setOnClickListener {
                repository.markAsRead(update.id)
                itemView.alpha = 0.5f // Визуальная отметка
            }

            container.addView(itemView)
        }

        return dialog
    }
    // Для адаптивности: полный экран на мобильных
    override fun onStart() {
        super.onStart()
        dialog?.window?.setBackgroundDrawableResource(R.drawable.dialog_background)
        dialog?.window?.setLayout(
            ViewGroup.LayoutParams.MATCH_PARENT,
            ViewGroup.LayoutParams.WRAP_CONTENT
        )
    }
}
