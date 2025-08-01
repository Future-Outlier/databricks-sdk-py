``w.clean_rooms``: Clean Rooms
==============================
.. currentmodule:: databricks.sdk.service.cleanrooms

.. py:class:: CleanRoomsAPI

    A clean room uses Delta Sharing and serverless compute to provide a secure and privacy-protecting
    environment where multiple parties can work together on sensitive enterprise data without direct access to
    each other's data.

    .. py:method:: create(clean_room: CleanRoom) -> Wait[CleanRoom]

        Create a new clean room with the specified collaborators. This method is asynchronous; the returned
        name field inside the clean_room field can be used to poll the clean room status, using the
        :method:cleanrooms/get method. When this method returns, the clean room will be in a PROVISIONING
        state, with only name, owner, comment, created_at and status populated. The clean room will be usable
        once it enters an ACTIVE state.

        The caller must be a metastore admin or have the **CREATE_CLEAN_ROOM** privilege on the metastore.

        :param clean_room: :class:`CleanRoom`

        :returns:
          Long-running operation waiter for :class:`CleanRoom`.
          See :method:wait_get_clean_room_active for more details.
        

    .. py:method:: create_and_wait(clean_room: CleanRoom, timeout: datetime.timedelta = 0:20:00) -> CleanRoom


    .. py:method:: create_output_catalog(clean_room_name: str, output_catalog: CleanRoomOutputCatalog) -> CreateCleanRoomOutputCatalogResponse

        Create the output catalog of the clean room.

        :param clean_room_name: str
          Name of the clean room.
        :param output_catalog: :class:`CleanRoomOutputCatalog`

        :returns: :class:`CreateCleanRoomOutputCatalogResponse`
        

    .. py:method:: delete(name: str)

        Delete a clean room. After deletion, the clean room will be removed from the metastore. If the other
        collaborators have not deleted the clean room, they will still have the clean room in their metastore,
        but it will be in a DELETED state and no operations other than deletion can be performed on it.

        :param name: str
          Name of the clean room.


        

    .. py:method:: get(name: str) -> CleanRoom

        Get the details of a clean room given its name.

        :param name: str

        :returns: :class:`CleanRoom`
        

    .. py:method:: list( [, page_size: Optional[int], page_token: Optional[str]]) -> Iterator[CleanRoom]

        Get a list of all clean rooms of the metastore. Only clean rooms the caller has access to are
        returned.

        :param page_size: int (optional)
          Maximum number of clean rooms to return (i.e., the page length). Defaults to 100.
        :param page_token: str (optional)
          Opaque pagination token to go to next page based on previous query.

        :returns: Iterator over :class:`CleanRoom`
        

    .. py:method:: update(name: str [, clean_room: Optional[CleanRoom]]) -> CleanRoom

        Update a clean room. The caller must be the owner of the clean room, have **MODIFY_CLEAN_ROOM**
        privilege, or be metastore admin.

        When the caller is a metastore admin, only the __owner__ field can be updated.

        :param name: str
          Name of the clean room.
        :param clean_room: :class:`CleanRoom` (optional)

        :returns: :class:`CleanRoom`
        

    .. py:method:: wait_get_clean_room_active(name: str, timeout: datetime.timedelta = 0:20:00, callback: Optional[Callable[[CleanRoom], None]]) -> CleanRoom
